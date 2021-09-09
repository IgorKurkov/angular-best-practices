# Angular Best Practices

# Description

This `Readme` and folder `./examples` describes collection of rules for the code style and architecture of `Angular` for any project.
The goal is to describe the minimum of best practices for angular while adhering to the 80/20 Pareto law.
This guide is crated for beginners in `Angular`.
So that a new programmer, without his training, write "correct" code and architecture.

This will free the team lead from training, which will make it easier for him to change staff.
Ultimately, this is necessary to comply with the principle - "Do it normally, and it will be fine."
Suggestions for improving this guide are welcome.

All examples are working. Examples from the `README` can be found in the project code.

Before starting to study a project, there are two things to keep in mind:

1. There are "unimportant things" - these are approaches in the development of refactoring which doesn't take much of time.
   For example, these include issues of naming folders, components, services, etc. It doesn't matter how exactly you'll call any files, and folders and etc, much more important is that you and your team should make it equally for all project.
2. There are "important things" - these are approaches in the development of which refactoring takes a lot of time, it is often easier to rewrite some logic than to refactor it. As a rule, these include issues of architecture, correct use of libraries and frameworks.

That's why you make "unimportant things" as you wish, but "important things" i suggest you do according to this manual .

Email: [evoytenkoapps@gmail.com](mailto:evoytenkoapps@gmail.com)

## Table of content

- [Files](#files)
- [Project structure](#project-structure)
- [Interfaces](#interfaces)
- [Formatting](#formatting)
- [Packages](#packages)
- [Lint](#Lint)
- [Git](#git)
- [TypeScript](#TypeScript)
- [JavaScript](#javascript)
- [Angular](#Angular)
  - [Мокируем сервисы](#мокируем-сервисы)
  - [Template](#Template)
- [RxJs](#RxJs)
- [Архитектура](#Архитектура)
- [Комментарии](#Комментарии)
- [CSS Стили](#css-стили)
- [Redux Store ( NGXS )](#Redux-Store--NGXS-)
- [Formly](#formly)

## Files

Try to store each class, interface, enum, record in different files. The file shouldn`t have more than one entity

For `interfaces` that describes methods we should create a file with ending `***.interface.ts` and name it `ISimple`

For `interfaces` that describes value object create a file with ending `***.ts` and name it like `Simple`

For `dictionary (record)` create a file with ending `***.dictionary.ts`

For `enum` `Simple` create a file with ending `***.enum.ts`

For `class` `Simple` create a file with ending `***.ts`

## Project structure

Split the project logic into the modules. Give them a name according to the business rules, without prefix `_`, fore example `user-info`

Group the folders inside module like this:

```
`_components` - components
    `_smart` - smart components
    `_dumb` - dumb components
`_providers` - providers
`_models` - models ( object value inetrfaces and classes )
`_pipes` - pipes
`_directives` - directives
`_guards` - guards
`_resolvers` - resolvers
`_store` - Redux ( ngxs example )
    `actions` = the models of actions
    `models` = the models of states and theris default values
    `states` =  the actions effects and their selectors
`_constants` - constants
`_services` - services
    `facade` - facade
    `api` - rest services
`user-info` - nested module
```

Give a name for nested modules by business logic.

`user-info`
`details`

Give a name for components modules by business logic without `_`

Mocks store inside production folders

For example: [project-folder-sturcture](https://github.com/evoytenkoapps/angular-best-practices/tree/master/examples/src/app/components/project-folder-sturcture)

```
├───user-info
│   │   user-info.module.ts
│   │
│   ├───user-software
│   ├───_components
│   │   ├───_dumb
│   │   │   └───user-info-details
│   │   │           user-info-details.component.css
│   │   │           user-info-details.component.html
│   │   │           user-info-details.component.spec.ts
│   │   │           user-info-details.component.ts
│   │   │
│   │   └───_smart
│   │       └───user-info
│   │               user-info.component.css
│   │               user-info.component.html
│   │               user-info.component.spec.ts
│   │               user-info.component.ts
│   │
│   ├───_constants
│   ├───_directives
│   ├───_guards
│   ├───_models
│   ├───_pipes
│   ├───_providers
│   │       uesr-http.provider.ts
│   │       user-info.provider.ts
│   │
│   ├───_resolvers
│   ├───_services
│   │   ├───api
│   │   │       user-http-mock.service.ts
│   │   │       user-http-prod.service.ts
│   │   │       user-http.service.ts
│   │   │
│   │   └───facade
│   │           user-ngxs.facade.ts
│   │           user.facade.ts
│   │
│   └───_store
│       ├───actions
│       ├───models
│       └───states
└───user-story
```

## Interfaces

For example for `environment` describe his interface `Environment` and store inside `./environments/models/environment.ts`

When interface uses only for one component, then we may store it inside component.

When interface uses for several component, then we should store it his owin file, like `./models/some-data`.

## Formatting

Use `prettier` for code formatting

Inside `./src` create a file and call it `.prettierrc.json`. Describe there all formatting settings as you wish. Probably your ide will offer you to apply them, so do it.

Inside `./src` create a file and call it `.prettierignore`. Describe there the paths for the files that you don't want to format

We configure the `IDE` so that formatting is applied to it on saving the file.

## Packages

Packages should be installed with opportunity to update the `patch` version. So you should set `~` before the package version in `package.json`, like `prettier": "~2.2.1`.
You may set it by default in `yarn` or `npm`.

## Lint

`Tslint` or `Eslint` should find code errors inside project for you. Use what the `Angular` version allows for you.

Install code check rules through third party packages, like `rxjs-tslint-rules`.

### Tslint

Add code check packages into `tslint.json`, property `extends`, like `"extends": ["tslint:recommended", "rxjs-tslint-rules"]`.
Then set what kind of rules you want to use. Add it inside property `rules`, like `"rxjs-no-unsafe-takeuntil": { "severity": "error" }`.

You may run code checking with command `ng lint --format prose`, and add it to `package.json`.

## Git

### CRLF LF

If you have git warning after use `git add .`, you may fix them inside file `.gitattributes`, add there a rule `* text=auto eol=lf`

## TypeScript

Use strict mode `"strict": true`

We specify access modifiers for all members and methods of classes.

We specify the data type for each property, constant, function argument, return value of a function, argument
functions `rxjs` operator exception complex operators` combine` and so on.

Try don't use optional setting operator `?`, like `private a?: number;`, because your code should be as strict as it is possible.

Don use type `any` ( possible use only when working with third-party libraries, if there is no possibility )

We avoid mutation of objects. To keep that you should add `readonly` modification to all properties of classes and interfaces. This will help avoid mutating data from
the child component of the parent and vice versa. Also, its help when working with `OnPush` strategies, because you'll should copy all objects for changes, and change their reference at the end.

Add `Readonly<X>` for any objects when you can't set `readonly` for his properties.

Wrong example:

```
requiremensDTO: IRequirementDTO[] = [];
const user = Readonly<User>
```

Nice example:

```
requiremensDTO: Readonly<IRequirementDTO>[] = [];
const user = Readonly<User>
```

Don't use `var`. Use `const` always, or `let` when you need to change reference.

Always use strict comparison `===`

When a class member will be not initialized inside constructor, for example value from `BehaviourSubject`, if strict mode is on `typescript`
will give an errors, then we mark it with the symbol `!`, otherwise we set `undefined` or` null`.

Example:

```
@Input() adress: string | undefined = undefined;

public userInfo!: UserInfo

ngOnInit(){
   this.userInfo$.pipe(takeUntil(this.destroy$)).subscribe(userInfo => this.userInfo = userInfo)
}
```

Don't call objects properties via string, because its break `DRY` principle.

Wrong code:

```
*ngIf="approveStatus['Deleted'] === 'deleted'"

this.router.navigate(['projects'])
```

Nice code:

```
*ngIf="status === approveStatus.Approved"
public approveStatus: typeof ApproveStatus = ApproveStatus;

this.router.navigate([Routes.PROJECTS])
```

Do not give the names of entities that begin with verbs, use nouns.

Wrong code:

```
export interface CreatePoTipInfoModel {
    header: string;
    message: string;
    }
```

Nice code:

```
export interface ProductOwnerTipInfoCreateModel {
    header: string;
    message: string;
    }
```

## JavaScript

Avoid `side effects`

If a function with an argument changes something, then we start calling it with the word `set`, like `setSometing(data: SomeType): void`

If a function without an argument changes something, then we call it from the word `change`, like `changeSometing(): void`

If a function gets a value, then we call it with the word `get`, whether there are arguments or not,
Examples

```
getSometing() : string
getSometing(data: SomeType) : string
```

Try to use array functions `filter`,` map`, `reduce`,` every`, `some` more often.
if you need to iterate over the array for the truth of a certain field
object and at the same time perform the action only if it is true, then
we use `find`. The code becomes cleaner and more readable.
For example, to change the array you do not need to use `foreEach + includes`, use` map + filter`

Wrong code:

```
  private getGroupTypes(filteredScoredContentEntries: ScoredContentEntry[]): GroupType[] {
    const groupTypes: GroupType[] = [];

    filteredScoredContentEntries.forEach((scoredContentEntry: ScoredContentEntry) => {
      const type: EntityResultItemType = this.getType(
        scoredContentEntry.contentEntry!.entityType as EntityType,
        scoredContentEntry.contentEntry!.entitySubType as number
      ) as EntityResultItemType;

      if (!groupTypes.includes(type.group)) {
        groupTypes.push(type.group);
      }
    });

    return groupTypes;
  }
```

Nice code:

```
  private getGroupTypes(filteredScoredContentEntries: ScoredContentEntry[]): GroupType[] {
    return filteredScoredContentEntries
      .map((scoredContentEntry: ScoredContentEntry) => {
        const type: EntityResultItemType = this.getType(
          scoredContentEntry.contentEntry!.entityType as EntityType,
          scoredContentEntry.contentEntry!.entitySubType as number
        );
        return type.group;
      })
      .filter((group, index, groups) => {
        return groups.indexOf(group) === index;
      });
  }
```

Wrong code:

```
    this.iterations = Object.keys(artifactNames).map(
      (key) => new ArtifactIteration(parseInt(key, 10), artifactNames[key as number])
    );
```

Nice code:

```
    this.iterations = Object.keys(artifactNames)
        .map((keyAsString) => parseInt(keyAsString, 10))
        .map((key) => new ArtifactIteration(key, artifactNames[key]));
```

Wrong code:

```
function getCurrentList(parentId: number, typeId: number): ArtifactType[] {
  let currentList = [];
  if (artifacts.allArtifacts.type.length > 0) {
    for (let artifactType of artifacts.allArtifacts.type) {
      if (artifactType.parentId === parentId) {
        currentList.push(artifactType);
      }
    }
  }
  currentList.sort((first, second) =>
    first.orderId < second.orderId ? -1 : 1
  );
  return currentList;
}
```

Nice code:

```
function getCurrentList(parentId: number, typeId: number): ArtifactType[] {
  return artifacts.allArtifacts.type
    .filter((artifactType) => artifactType.parentId === parentId)
    .sort((first, second) => (first.orderId < second.orderId ? -1 : 1));
}
```

Inside arrow functions, specify the name of the arguments according to logic, like `countersDTO`, ` maxDate`.
It would be clear to understand what they contain, for example . Don't call them unreadable, like `c`,`m`

Wrong code:
`if(arr.find( u => u.userName === 'Петрович' ))`

Nice code:
`if(users.find( user: User => user.userName === 'Петрович' ))`

All booleans values start to call with `is` or `has`

Wrong code:

```
showDeleted: boolean
```

Nice code:

```
isShowDeleted: boolean
```

Try don't give the simple names ( double interpretation ) to methods, properties, classes that makes specific things. For example, instead of `count` or` allItemsCount`, we try to use `totalFoundInSearch`, instead of` isEdit` -> `isShowDeleteAndCancel`

Don't use more than one ternary operator`?` at once. Instead, check it inside `if() {return} return`.
Wrong code:

```
return link.includes('groups')
      ? FDM_SEARCH_RESULT_GROUP.GROUPS
      : link.includes('domains')
      ? FDM_SEARCH_RESULT_GROUP.DOMAINS
      : link.includes('business-capabilities')
      ? FDM_SEARCH_RESULT_GROUP.BUSINESS_CAPABILITIES
      : FDM_SEARCH_RESULT_GROUP.GROUPS;
```

Nice code:

```
 if(link.includes('groups'))
    return FDM_SEARCH_RESULT_GROUP.GROUPS
 if(link.includes('domains'))
    return FDM_SEARCH_RESULT_GROUP.DOMAINS
 if(link.includes('business-capabilities'))
    return FDM_SEARCH_RESULT_GROUP.BUSINESS_CAPABILITIES
 return FDM_SEARCH_RESULT_GROUP.GROUPS
```

Don't use expressions over than 70 characters in arrays, object values, if() etc. Move them into separate constants or functions. When we assign expressions to constants, we increase their understanding and readability, and such code is much more easier to debug.

Wrong code:

```
    return {
      [FDM_SEARCH_RESULT_GROUP.GROUPS]: state.searchResults[FDM_SEARCH_RESULT_GROUP.GROUPS].filter(
        (domain) => domain.status !== DomainDTOStatus.Deleted
      ),
      [FDM_SEARCH_RESULT_GROUP.DOMAINS]: state.searchResults[FDM_SEARCH_RESULT_GROUP.DOMAINS].filter(
        (domain) => domain.status !== DomainDTOStatus.Deleted
      ),
      [FDM_SEARCH_RESULT_GROUP.BUSINESS_CAPABILITIES]: state.searchResults[
        FDM_SEARCH_RESULT_GROUP.BUSINESS_CAPABILITIES
      ].filter((capability) => capability.status !== CapabilityDTOStatus.Deleted),
      [FDM_SEARCH_RESULT_GROUP.TECH_CAPABILITIES]: state.searchResults[
        FDM_SEARCH_RESULT_GROUP.TECH_CAPABILITIES
      ].filter((capability) => capability.status !== CapabilityDTOStatus.Deleted),
    } as FdmSearchResults;
```

Nice code:

```
    const groups: DomainDTO[] = state.searchResults[FDM_SEARCH_RESULT_GROUP.GROUPS];
    const deletedDGroups: DomainDTO[] = groups.filter((domain) => domain.status !== DomainDTOStatus.Deleted);

    const domains: DomainDTO[] = state.searchResults[FDM_SEARCH_RESULT_GROUP.DOMAINS];
    const deletedDDomains: DomainDTO[] = domains.filter((domain) => domain.status !== DomainDTOStatus.Deleted);

    const businessCapabilities: CapabilityDTO[] = state.searchResults[FDM_SEARCH_RESULT_GROUP.BUSINESS_CAPABILITIES];
    const deletedBusinessCapabilities: CapabilityDTO[] = businessCapabilities.filter(
      (capability) => capability.status !== CapabilityDTOStatus.Deleted
    );

    const techCapabilities: CapabilityDTO[] = state.searchResults[FDM_SEARCH_RESULT_GROUP.TECH_CAPABILITIES];
    const deletedTechCapabilities: CapabilityDTO[] = techCapabilities.filter(
      (capability) => capability.status !== CapabilityDTOStatus.Deleted
    );

    return {
      [FDM_SEARCH_RESULT_GROUP.GROUPS]: deletedDGroups,
      [FDM_SEARCH_RESULT_GROUP.DOMAINS]: deletedDDomains,
      [FDM_SEARCH_RESULT_GROUP.BUSINESS_CAPABILITIES]: deletedBusinessCapabilities,
      [FDM_SEARCH_RESULT_GROUP.TECH_CAPABILITIES]: deletedTechCapabilities,
    } as FdmSearchResults;
```

Wrong code:

```
    if (
      (typeof data.currentValue && typeof data.previousValue) === 'string' &&
      (data.currentValue ? data.currentValue : '').length + data.previousValue.length > 0 &&
      data.key !== 'owner' &&
      data.key !== 'creationDate' &&
      data.key !== 'lastChangeDate' &&
      data.key !== 'type' &&
      data.key !== 'incomingLinksData' &&
      data.key !== 'status' &&
      data.key !== 'licensesData' &&
      data.key !== 'licenses' &&
      data.key !== 'tools' &&
      data.key !== 'toolsData'
    )
```

Nice code:

```
    const isValueIsString: boolean = (typeof data.currentValue && typeof data.previousValue) === 'string';
    const currentValue: number = data.currentValue ? data.currentValue.length : 0
    const isLengthNotZero: number = currentValue + data.previousValue.length > 0
    const isKeyNotExist: boolean =
      data.key !== 'owner' &&
      data.key !== 'creationDate' &&
      data.key !== 'lastChangeDate' &&
      data.key !== 'type' &&
      data.key !== 'incomingLinksData' &&
      data.key !== 'status' &&
      data.key !== 'licensesData' &&
      data.key !== 'licenses' &&
      data.key !== 'tools' &&
      data.key !== 'toolsData';

    if (isValueIsString && isLengthNotZero && isKeyNotExist)
```

Nice code:

```
 private filterList<T extends DomainDTO | CapabilityDTO>(list: T[], filters: FdmSearchFilters): T[] {
    return list.filter((entity): boolean => {
      const isCodeFound: boolean = !!entity.code?.toLowerCase().includes(filters.search.toLowerCase());
      const isNameFound: boolean = !!entity.name?.toLowerCase().includes(filters.search.toLowerCase());
      const isOwnerEqual: boolean = entity.owner === filters.owner?.rmsId;
      if (filters.search && filters.owner) {
        return (isCodeFound || isNameFound) && isOwnerEqual;
      }
      if (filters.owner) {
        return isOwnerEqual;
      }
      if (filters.search) {
        return isCodeFound || isNameFound;
      }
      return false;
    });
```

Instead of `Record`, we try to use the interface as an associative array, because you can specify the names of properties in it, which
will increase the readability of the code.

Wrong code:

```
sectionsCounters: Record<number, SectionCounters>;
```

Nice code:

```
sectionsCounters: { [classifierValueId: number]: SectionCounters }
```

Inside the method, you need to use only one nesting of curly braces, otherwise make an alternate of `if () {}` with nesting 1 or split the method into several methods.
look here https://www.youtube.com/watch?v=AkdEsCHt1cg&t=166s
Wrong code:

```
  @Action(AlertifyError)
  public alertifyError({}: StateContext<AlertifyStateModel>, { error }: AlertifyError): void {
    let message: string;
    if (error instanceof Error) {
    if (error instanceof ApiException) {
      if (error.response) {
        try {
          const parsedApiErrorResponse: { Message?: string } = JSON.parse(error.response);
          if (parsedApiErrorResponse && parsedApiErrorResponse.Message) {
            message = parsedApiErrorResponse.Message;
          } else {
            message = error.message;
          }
        } catch (_parseApiErrorResponseError) {
          message = error.message;
        }
      } else {
        message = error.message;
      }
    } else if (error instanceof Error) {
      message = error.message;
    } else {
      message = error;
    }
```

Nice code:

```
  @Action(AlertifyError)
  public alertifyError({}: StateContext<AlertifyStateModel>, { error }: AlertifyError): void {
    const message: string = this.getErrorMessage(error);
    AlertifyService.error(message);
  }

    private getErrorMessage(error: ApiException | Error | string): string {
    if (error instanceof ApiException) {
      return this.getApiErrorMessage(error);
    }
    if (error instanceof Error) {
      return error.message;
    }
    return error;
  }

    private getApiErrorMessage(error: ApiException): string {
    const parsedApiErrorMessage = this.tryParseApiErrorMessage(error.response);
    if (parsedApiErrorMessage !== null) {
      return parsedApiErrorMessage;
    }
    return error.message;
  }

    private tryParseApiErrorMessage(response: string): string | null {
    try {
      const parsedApiErrorResponse: { Message?: string } = JSON.parse(response);
      if (parsedApiErrorResponse && parsedApiErrorResponse.Message) {
        return parsedApiErrorResponse.Message;
      }
    } catch (_parseApiErrorResponseError) {}
    return null;
  }

```

Instead of `if else`, use `if return return`
Wrong code:

```
    if (!isReleaseExists && !isCacheExists) {
      return new ReleaseDTO();
    } else {
      return drafts[key];
    }
```

Nice code:

```
    if (!isReleaseExists && !isCacheExists) {
      return new ReleaseDTO();
    }
    return drafts[key];
```

We adhere to the law of `Demeter`. In other words, when accessing an object, a service, we use only one dot notation, like `someObject.someProperty`

We comply with the `DRY` law. In other words, do not use the same text, expression, piece of code twice. We move them into constants, `Enum`, `Class`, `function` etc ...

Mutations:

1. We don't make mutations inside components, it may cause problems with `onPush` strategy.
2. We do not change references to object`s properties from nested functions. Try to do that where object initialized. If the object is a member of the class, then
it is desirable to change it inside called function. 

Wrong code:

```
const a = {....}
  f1() {
    f2(){
      f3() { a.property = true }
      }
    }
```

Nice code:

```
  let a = {....}
  const property: boolean = f1();
  a = {...a, aSomeFiled: property }

  f1() { return f2(); }
  f2(){ return f3(); }
  f3(){ return true }

```

## Angular

We use the `OnPush` strategy for all components by default. To do this by default, we specify this rule in `angular.json`

```
        "@schematics/angular:component": {
          "changeDetection": "OnPush"
        }
```

Follow by `the single responsobility principle` we split large components, services, templates into several smaller ones, they are easier to test and more pleasant to maintain.
We strive for `75` lines of code in the` html` template, otherwise we split it into several smaller ones (`smart` +` dumbs`).
We strive to `400` lines of code in components, services, directives, otherwise we break them down into several more
small.

We don't use `Promise`, only` RxJS Observables`.

We do not inherit components from each other. If you need to bring the general into the code, then we use: services, directives, parent class etc.

We use the `trackBy` function for all` ngFor`. (see. `TrackByExampleComponent`)

We avoid cyclical dependencies of entities (services, classes). If they arise, and essence A depends on B, and B depends on A, then we aggregate them inside essence C (A, B). And after all we use C.

We give the names `Input`, `Output` so that it is clear from the outside which one they were performing.

Wrong code:

```
      <sol-release-details-actions
        [editMode]="isEdit"
        [canEdit]="true"
        [canDelete]="false"
        [canSave]="true"
        [canCancel]="true"
        [isDraftValid]="isDraftValid$ | async"
        (cancel)="onCancel()"
        (save)="onCreate()"
      ></sol-release-details-actions>
```

Nice code:

```
      <sol-release-details-actions
        [isShowEditAndDelete]="!isEdit"
        [isShowEdit]="true"
        [isShowDelete]="false"
        [isShowSave]="true"
        [isShowCancel]="true"
        [isSaveEnable]="isFormValid"
        (cancel)="onCancel()"
        (save)="onCreate()"
        (edit)="onEdit(release)"
      ></sol-release-details-actions>
```

For `dumb's` ` Input`, `Model`,` Output` names, we do not transfer the business logic from smart and vice versa.

Wrong code:

```
  [isDraftValid]="isDraftValid$ | async"
```

Nice code:

```
<app-dumb>
  [isSaveEnable]="isDraftValid$ | async"
</app-dumb>
```

Придерживаемся следующего порядка объявлений свойств контроллера компонента:

```
view child (property)
input (property)
output (property)
selector (property)
disaptch (property)
public (property)
private (property)
constructor()
public (method)
private (method)
```

При создании объектов придерживаемся подхода ООП . Т.к `Angular` расчитан на ООП, в нем испольузются подходы ООП.
Поэтому не создаем объкты через функцию, а делаем классы.
Wrong code:

```
  public licenseMock = (license?: Partial<ILicenseDTO>): ILicenseDTO => {
    const mock: ILicenseDTO = {
      id: license?.id || this.randomService.id(this.mockDataSyncService.licenseMap.ids),
      name: license?.name || this.randomService.title(),
      description: license?.description || this.randomService.description()
    };
    return mock;
  };
```

Nice code:

```
  public licenseMock = new LicenseMock(license?: Partial<ILicenseDTO>);
```

Не используйте аббревиатуры в названии компонентов, давайте полное название, развернутое название.

Wrong code:
`PoStepsCreateComponent`

Nice code:
`ProductOwnerStepsCreateComponent`

Не называйте компоненты с глаголов, начинайте название с бизнес сущности.

Wrong code:
`CreatePoStepsComponent`

Nice code:
`ProductOwnerStepsCreateComponent`

Не назначайте свойствам названия начинающихся с глаголов, давай с существительных, либо `is`.
Wrong code:

```
    @Input() createPoTipInfo: ProductOwnerTipInfoModel = {
        header: '',
        message: '',
    };
```

Nice code:

```
    @Input() productOwnerTipInfo: ProductOwnerTipInfoModel = {
        header: '',
        message: '',
    };
```

Если аргумент функции, результат функции, свойство класса, интерфейса и т.д могу быть `null` или `undefined`, то указываем это явно. Нужно показывать что вы ожидаете или не ожидаете получить, возвратить `null` или `unefined (void)`.

Wrong code:

```
@Input() userName: string;
....
if(this.userName){
    .....
}
```

Nice code:

```
@Input() userName: string | null = null
....
if(this.userName){
    .....
}
```

Если вам нужно отслеживать изменения в `@Input()`, например запускать какую-либо логику, то вы можете для этого использовать `setter`. Использовать для этого `OnChanges` не рекомендуется, т.к по умолчанию он не поддерживает проверку типов, и это может привести к ошибкам при рефакторинге инпута.
Если у вас может возникнуть `glitch` эффект, то лучше использовать `ngOnChanges`, но при этом вам обязательно нужно обернуть `SimpleChanges` в `Generic`. Пример обертки смотрите тут [input-changes-detection](https://github.com/evoytenkoapps/angular-best-practices/tree/master/examples/src/app/components/input-changes-detection)

Wrong code:

```
  ngOnChanges(changes: SimpleChanges): void {
    const name = changes.userName?.currentValue;
    if(name){
        console.log('name inside changes was changed', name);
        this.userName = name;
    }
  }
```

Nice code:

```
  @Input()
  set userName(name: string | null) {
    console.log('name inside input was changed', name);
    if (name) {
      this.firstName = name;
    }
  }

  public firstName: string = '';
```

Давайте для`Input\Output` такие названия, чтобы снаружи можно было понять какую работу они выполняют. В результате это должно быть понятно без их просмотра.

When you need to update or init data of any `ui` element, for example `mat-table`, you have to keep in mind, that this `ui` element creates after calling `ngAfterViewInit` life hook.
So to update its data you need to:

1. Store data inside parent component controller, inside `@Input()` , `subscription` or etc
2. Check is `ui` exist, then update its data
3. Set `ui` data inside `ngAfterViewInit`

Wrong example:

```
  @Input() set methods(methods: IMethodDTO) {
       this._methods = methods;

       this.setParametersDataSource(this._methods.parameters);
  }
```

Good example:

```
  @Input() set methods(methods: IMethodDTO) {
       this._methods = methods;

       if(this.tableParametrs){
          this.setParametersDataSource(this._methods.parameters);
        }
  }

  public ngAfterViewInit(): void {
      if(this.this._methods){
          this.setParametersDataSource(this._methods.parameters);
        }
  }

```

### Мокируем сервисы

Для того чтобы не зависеть от стороннего сервиса, например от бекенда, и получать любые данные, какие мы хотим, в
любой момент времени, мокируем получение данных.

1. Создаем базовый абстрактный класс`abstract class LoggerService`, описываем в нем нужные методы
2. Создаем нужный нам сервис `class MyLoggerService extends LoggerService `, наследуемся от абстрактного и прописываем
   нужную реализацию.
3. Создаем `MyLoggerMockService` сервис, наследуемся от абстрактного и прописываем нужную реализацию. В названии в начале
   ставим слово `Моск`. Файл называем по маске `*****-mock.service.ts`
4. Инжектируем абстрактный класс `LoggerService` в компоненты
5. Создаем провайдер `LoggerServiceProvider` в отдельном файле. Пишем содержимое провайдера `export const LoggerServiceProvider: Provider = { provide: LoggerService, useValue: environment.isUseLogger ? new MyLoggerMockService() : new MyLoggerService(), };`. Прописываем в providers условия выбора `Production` или `Mock`. Используем `useClass`
   или `useFactory`
6. Вставляем провайдер в модуль `providers: [LoggerServiceProvider]`
7. provider храним в папке `Providers` данного модуля (где они используются)
8. `Mock` кладем рядом с продакшн классами, в ту же папку, или того же родителя, но в другую папку.
9. В объекты ( компоненты, сервисы ) нужно инжектировать абстракции, а не реальные реализации. Т.к передача реализаций нарушает принцип инверсии зависимостей.

### Template

Атрибуты компонента, или тега указываем в следующем порядке:

1. все директивы
2. статичные атрибуты
3. inputs
4. outputs

Пример:

```
<app-component *ngIf="true" id="1" class="app-component"  [data]="data" (data)=setData($event)>
</app-component>
```

Для каждого компонента, где необходимо, стараемся создавать свою собственную модель. Мапить ее необходимо в компоненте выше, как на для Input, так и при получении из Output.
Например если у родителя объект с 5 свойствами, а потомку нужно только 4 свойства, то в потомке нужно создать собсвенный интерфейс с этими 4 полями и ждять его на вход. Преобразование 5 в 4 должен делать его родитель.
(parent m1 to m2) m2 -> child, child m2 -> (m2 to m1 parent)

## RxJs

В компоненте всегда делаем отписку от `subscribe()`. Если в компоненте нет подписки с помощью `subscribe()`, то отписку
делать бессмысленно. Wrong code:

```
    this.uneditable$ = this.api.getClassifiersTopShowOnGUI().pipe(
      map((response) => response.result),
      takeUntil(this.destroy$)
    );
```

В целях отписки, оператор `takeUntil(.....)` нужно ставить непосредственно рядом с `subscribe()`, ставить его выше не
безопасно.

```
    this.uneditable$ = this.api.getClassifiersTopShowOnGUI().pipe(
      map((response) => response.result),
      takeUntil(this.destroy$)
    ).subscribe();
```

Отписку делаем с помощью `takeUntil()` + ( `Subject` или `UnsubscribeService` )

Пример:

```
.pipe(
  .map(....)
  tap(.....),
  takeUntil(this.destroyer)
)
.subscribe(() => ....);
```

Не делаем подписки в конструкторе, вместо этого делаем их в `OnInit` или `AfterViewInit` по ситуации.

Wrong code:

```
  constructor(
    private supportService: SupportService,
    private unsubscribeService$: UnsubscribeService
  ) {
    this.supportService.commonSupportAvailableState$.pipe(takeUntil(this.unsubscribeService$)).subscribe((state) => {
      this.isCommonSupportAvailable = state;
    });
  }
```

Пример лучше:

```
  ngOnInit(){
    this.supportService.commonSupportAvailableState$.pipe(takeUntil(this.unsubscribeService$)).subscribe((state) => {
      this.isCommonSupportAvailable = state;
    });
  }
```

Подписку `.subscribe(() => ....)` внутри другой подписки `.subscribe(() => subscribe())` делать нельзя. Если надо
получить данные из другого потока, то используем `switchMap` либо другие операторы высшего порядка. Wrong code:

```
    // Первая подписка
    this.isModuleEditor$.pipe(takeUntil(this.destroy$)).subscribe((access) => {
        this.draftsService
          .getDrafts(DraftStatuses.Created, this.user.userId)
          .pipe(takeUntil(this.destroy$))
          // Подписка в подписке
          .subscribe((result) => {
            if (result) {
              this.containersService.pendingDraftState.next(result ? result : []);
            }
          });
    });
```

В целях избегания `side effects` стараемся не вызывать в потоке `subject.next`. Вместо использования `subject` выносим
общую часть потока в `pipe()` и используем ее. Далее расширяем общую часть операторами.
Например: `subjectAnalog$ = dataSourse$.pipe(....); otherData$ = subjectAnalog$.pipe(.....)`

В сервисах и компонентах разрешается делать присваивание или вызов других методов только в операторах `tap`
либо `subscribe`.

В компонентах желательно делать присваивание или вызов других методов в `subscribe` вместо `tap`, иначе мы получим не
явный `side effect`.

Wrong code:

```
  this.rmsEntitiesService.rmsContoursState$ .pipe(
    tap((contours) => {
      if (!contours) {
        this.getRmsContours();
      }
    }),
  takeUntil(this.destroy$)
  ).subscribe()
```

Правильный пример:

```
  this.rmsEntitiesService.rmsContoursState$ .pipe(
  filter (contours => !contours)),
  takeUntil(this.destroy$))
  .subscribe(() => this.getRmsContours()
  )
```

Если в методе нужно получить данные из другого потока, то не нужно создавать подписку в методе. Делаем так:

1. создаем `subject`
2. подписываемся на него в `ngOnInit`, прописываем в его `pipe()` нужный поток с помощью операторов высшего порядка,
   например `switchMap`.
3. в методе вызываем `subject.next()`
4. получаем данные в `subscribe()`, либо через ` | async`

Пример:

```
// Создаем потоки
const sub = new Subject();
const data$ = of(1);

// Подписываемся в
ngOnInit{
  sub.pipe(switchMap(_ => data$),takeUntil(this.destroy$)).subscribe(console.log);
}

// Вызываем в методе
public onClick(){
  this.sub.next();
}
```

Вместо `setTimeout()` лучше использовать `Subject.subscribe()` + оператор `delay`
Wrong code:

```
  getClassifications() {
    setTimeout(() => {
        this.initFilters();
    }, 100);
  }
```

Не делаем подписки в методах, которые часто вызываются фреймворком, например `ngOnChanges`

Wrong code:

```
  ngOnChanges(changes: SimpleChanges): void {
      this.projectsService
        .getProject()
        .pipe(takeUntil(this.unsubscribeService$))
        .subscribe();
  }
```

Не передавайте (Observable, Subject, etc...) как аргументы в функции и не полчайте результат работы даннх функций. Вместо этого вызывайте эти функции по цепочке, используя `pipe` + операторы
Wrong code:
Тут мы получаем поток `itemsTypesWhereCountsIsGreaterThanZero` как результат функции, а затем передаем его как аргумент в другую функцию `_getFilterModelFromItemTypes`.
Вместо этого можно использовать их по цепочке

```
  public getFilterModel(searchText: string): Observable<FilterModel> {
  .......
      const itemsTypesWhereCountsIsGreaterThanZero: Observable<
        ItemType[]
      > = this._getItemsTypesWhereCountsIsGreaterThanZero(allItemsTypesWithCounts);

      const filterModel: Observable<FilterModel> = this._getFilterModelFromItemTypes(
        itemsTypesWhereCountsIsGreaterThanZero
      );

      return filterModel;
    });
  }

  private _getItemsTypesWhereCountsIsGreaterThanZero(
    allItemsTypesWithCounts: Observable<ItemTypeWithTotalCount>[]
  ): Observable<ItemType[]> {
    return forkJoin(allItemsTypesWithCounts).pipe(
      map((itemsTypeWithCount: ItemTypeWithTotalCount[]) => .....
      )
    );
  }

    private _getFilterModelFromItemTypes(itemsTypesWhereCountsIsGreaterThanZero: Observable<ItemType[]>
  ): Observable<FilterModel> {
    return itemsTypesWhereCountsIsGreaterThanZero.pipe(
      map((itemsTypesWithCount: ItemType[]) => {
        ....
      })
    );
  }
```

Этот пример лучше:

```
  public getFilterModel(searchText: string): Observable<FilterModel> {
   .......
   return this._getItemsTypesWhereCountsIsGreaterThanZero(allItemsTypesWithCounts).pipe(
    switchMap((itemsTypesWhereCountsIsGreaterThanZero) => this._getFilterModelFromItemTypes( itemsTypesWhereCountsIsGreaterThanZero))
    )
    });
  }

  private _getItemsTypesWhereCountsIsGreaterThanZero(
    allItemsTypesWithCounts: Observable<ItemTypeWithTotalCount>[]
  ): Observable<ItemType[]> {
    return forkJoin(allItemsTypesWithCounts).pipe(
      map((itemsTypeWithCount: ItemTypeWithTotalCount[]) => .....
      )
    );
  }

    private _getFilterModelFromItemTypes(itemsTypesWhereCountsIsGreaterThanZero: Observable<ItemType[]>
  ): Observable<FilterModel> {
    return itemsTypesWhereCountsIsGreaterThanZero.pipe(
      map((itemsTypesWithCount: ItemType[]) => {
        ....
      })
    );
  }
```

## Архитектура

Придерживаемся концепции `smart + dumbs components` (умный / глупый компоненты) см. [smart-dumb-concept](https://github.com/evoytenkoapps/angular-best-practices/tree/master/examples/src/app/components/smart-dumb-concept)

`smart` - умный.

1. Только он общается со сторонними сервисами, например `http-facade` `store-facade` и т.д. Общение со сторонними сервисами происходит только через абстракции.
1. Содержит в себе бизнес логику.
1. Отвечает за роутинг.
1. Не использует `Input\Output`.
1. Может показывать данные.

`dumb` - глупый.

1. Показывает данные.
1. Передает, показывает данные только родителя.
1. Использует минимум логики внутри.
1. Не использует сервисы.
1. Содержит логику обработки вложенных компонентов.
1. Использует `Input\Output`.

В одном умном максимально вложено 5 глупых, например: `(smart(dumb1(dumb2(dumb3(dumb4(dumb5))))))`, при большем
количестве будет сложно поддерживать `Input, Output, @ViewChild()`

Передачу данных между `родитель - потомок ` делаем через `input + output`

Если родителю нужно послать потомку событие или данные, в родителе используем `@ViewChild()` + вызов метода потомка.

Сущности разбиваем на три типа:

1. `DTO` - то что приходит, уходит на бэкенд `DataDTO`
2. `Entity` - то что хранится в store `Data`, используем его как `value object`, то есть он должен быть без методов.
3. `Vm` - то что нужно для компонента. `VmData`

Для `Entity` не используем класс или интерфейс с методами, используем собственный интерфейс `Data` или интерфейс `IData` из `swagger`, при этом чтобы в них не было методов.

Не давайте названия свойствам `dumb` компонента по бизнес логике. Старайтесь давать абстрактные названия по логике `dumb`
Wrong code:

```
    @Output() removeComponent: EventEmitter<void> = new EventEmitter<void>();
```

Nice code:

```
    @Output() deleteBtnChange: EventEmitter<void> = new EventEmitter<void>();
```

## Комментарии

Если в коде есть бага или особенность которую, к сожалению, невозможно понять из кода, то комментируем ее, либо делаем TODO. В других случаях комментарии писать не нужно, нужно стараться давать однозначные для понимания названия для сущностей и функций. Избегать двойных трактований. Чтобы в итоге получить само-документируемый код. Сам код должен читаться как хорошая книга о вашей логике.

Wrong code:

```
// Передаем null в дерево
if (!moduleObject && !apiInterfaceObject && this.slCheckTreeService) {
  this.slCheckTreeService.selectNode(null);
}
```

Nice code:

```
// Удаляем выбранные элементы из дерева когда ничего не выбрано
if (!moduleObject && !apiInterfaceObject && this.slCheckTreeService) {
  this.slCheckTreeService.selectNode(null);
}
```

Nice code:

```
// Тут нюанс ngxs, т.к она работает вне зоны, диалог не будет закрываться. Нужно вызывать диалог в зоне см. https://github.com/ngxs/store/issues/1401#issuecomment-545180014
this.ngZone.run(() => {
  this.dialog.open(ConfirmationModalComponent, {
    panelClass: 'custom-dialog-container',
    data: infoData,
  });
});
```

## CSS Стили

Стили компонента указываем в файле стилей компонента `*.component.scss`

Стили для "root" элемента компонента указываем в файле стилей, в псевдо-классе `host`

Придерживаемся методологии BEM

Пример:

```
   main-button
   main-button--primary
   main-button__label
   main-button__label--secondary
```

Для облегчения верстки у компонентов, в `*.css` выставляем по умолчанию `:host {display: block}`. Чтобы сделать это по умолчанию у новых компонентов создаваемых через `ng g c` указываем это правило в `angular.json`

```
        "@schematics/angular:component": {
          "displayBlock": true
        }
```

**SVG**

Монохром:
Временно храним их в `assets`

Не монохром:

1. Без логики - храним в `assets`
2. С логикой - создаем отдельный компонент и храним код `svg` в нем

## Redux Store ( NGXS )

См. пример реализации [redux-store-ngxs](https://github.com/evoytenkoapps/angular-best-practices/tree/master/examples/src/app/redux-store-ngxs)

Сущности храним в папках:

`actions` = классы actions
`models` = интерфейсы, классы стейтов и их дефолтные значения
`states` = эффекты actions и селекторы

Если нужно отслеживать статус какого-либо объекта в `store`, то мы оборачиваем его в `Generic`:

```
export interface StoreStatusData<T> {
  data: T;
  status: StoreStatus;
}
```

При реализации `Action` воспроизводить все возможные случаи и смотреть как их отрабатывает проект.

Пример:

1. Нет данных,
2. Есть 1 объект,
3. Есть 1000 объектов
4. Ошибка
5. Есть 1 объект задержка 5 сек
6. Все основные комбинации связанных `Action`.

Если есть возможность делаем собственные селекторы для каждого `smart` компонента.

Не делаем общий селектор для нескольких `smart`, если эти смарты не влияют друг на друга по бизнес логике. Иначе можно
сделать единый селектор. Либо объединить несколько селекторов через операторы `merge` и т.д

Wrong code:

```
    @Selector()
  public static active(state: ReleaseDetailsStateModel) {
    const { initial, drafts } = state;
    const key = `${initial?.id ?? NEW_KEY}`;
    const isReleaseExists = !!initial && initial.id > 0;
    const isCacheExists = drafts.hasOwnProperty(key);
    console.log('isReleaseExists', isReleaseExists, 'isCacheExists', isCacheExists);
    if (!isReleaseExists && !isCacheExists) {
      return new ReleaseDTO();
    } else if (!isReleaseExists && isCacheExists) {
      return drafts[key];
    } else if (isReleaseExists && !isCacheExists) {
      return initial;
    } else {
      return drafts[key];
    }
  }
```

Nice code:

```
  @Selector()
  public static getSelectedRelease(state: ReleaseDetailsStateModel): ReleaseDTO | null {
    const { drafts } = state;
    const selected: ReleaseDTO | null = state.initial;
    const draft: ReleaseDTO | null = selected ? drafts[selected.id] : null;
    return draft ? draft : selected;
  }

  @Selector()
  public static getNewReleaseDraft(state: ReleaseDetailsStateModel): ReleaseDTO | null {
    return state.drafts[ReleaseDetailsState.NEW_RELEASE_ID];
  }

    @Selector()
  public static isSelectedReleaseCached(state: ReleaseDetailsStateModel): boolean {
    const selected: ReleaseDTO | null = state.initial;
    return selected ? !!state.drafts[selected.id] : false;
  }
```

Даем названия для `actions` так же как и для функций, начинаем с глагола. Wrong code:

```
NewRelease
```

Nice code:

```
ResetSelectedRelease
```

В Store храним данные, только если они нужны после создания компонента, но были получены до его создания.
Если данные не храним в `store`, то для получения данных из эффектов используем `Actions` (как шину данных).
Пример:

```
ngOnInit(): void {
  this.actions$
    .pipe(
      ofActionSuccessful(GetSearchResultSuccess),
      takeUntil(this.unsubscribeService)
      )
    .subscribe((searchResult: { fullInfo: ScoredContentEntry[] }) => {
      this.searchResult = this.globalSearchService.getSearchResult(searchResult.fullInfo);
  });
}
```

```
  canActivate(next: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<boolean | UrlTree> {
    this.store.dispatch(new LoadRelease(id));

    const loaded$: Observable<boolean> = this.actions$.pipe(
      ofActionDispatched(LoadReleaseLoaded),
      map(() => true)
    );

    const error$: Observable<boolean> = this.actions$.pipe(
      ofActionDispatched(LoadReleaseError),
      map(() => {
        this.redirectToErrorPage();
        return false;
      })
    );

    return merge(loaded$, error$).pipe(take(1));
  }

```

`moment` Показывается в `Redux dev tools` как строка.

Делаем все взаимодействие с `Store` через абстрактный класс, называем его `***.facade.ts`, например `UserInfoFacade` `user-info.facade.ts`, делаем по аналогии с мокированием сервисов.
Провайдим фасад на уровне модуля.
В компонент инжектим абстрактный класс.
В итоге компонент не должен иметь импорты на библиотеки `Redux Store`.

Давайте абстрактные названия методам фасада, по бизнес логике, не нужно в него приносить термины используемые в текущей `store`.
За основу можете взять глаголы "Create Read Update Delete Set Get Change Update Load" + бизнес сущность.

Wrong code:

```
public abstract selectStatus(): Observable<StoreStatus>;
public abstract ofActionGetFormDataFromLocalStorageSuccessDispatched(): Observable<ICreatePOStepsModel>;
```

Nice code:

```
public abstract getStatus(): Observable<StoreStatus>;
public abstract loadedStepsFromLocalStorage(): Observable<ICreatePOStepsModel>;
```

Т.к по умолчанию `ngxs` работает вне `ngZone`, поэтому если вам нужно будет показать диалоги, или прочие `ui` компоненты из `action`, то лучше это делать внутри `ngZone` явно.

Wrong code:

```
  @Action(AuthorizeError)
  public authorizeError({ setState, dispatch }: StateContext<AuthStateModel>, { error }: AuthorizeError): void {
         this.dialog.open(ConfirmationModalComponent, {
            panelClass: 'custom-dialog-container'
    }
  }
```

Nice code:

```
  @Action(AuthorizeError)
  public authorizeError({ setState, dispatch }: StateContext<AuthStateModel>, { error }: AuthorizeError): void {
     this.ngZone.run(() => {
        this.dialog.open(ConfirmationModalComponent, {
        panelClass: 'custom-dialog-container'
      });
    });
  }
```

## Formly

Если вам не нужно менять всю `Entity` то не передаем его полностью в модель, а обязательно защищаем модель собственным интерфейсом. Для этого создаем его, либо пикаем из другого.
Пример пика:

```
export interface ReleaseFormModel
  extends Pick<
    IReleaseDTO,
    'name' | 'position' | 'description' | 'rmsReleaseId' | 'businessUnitId' | 'dateFrom' | 'dateTo' | 'installDate'
  > {}
```

Обязательно объявляем модель по умолчанию и инициализируем ее внутри формы. Иначе форма будет эмитить модель с одним свойством в первый раз, что приведет к ошибкам. Делаем защиту от дурака.

Задаем модель через `setter` с обязательной проверкой на `null` и клонированием, тем самым мы делаем защиту от дурака, т.к `formly` мутирует объект в рантайме, если модель прилетит из `store`, то будет ошибка. Т.к `store` как правило фризит свои модели

```
  @Input() set model(model: ReleaseFormModel | null) {
    if (model) {
      this._model = { ...model };
    }
  }
```

Обязательно устанавливаем значения ключей форм из модели с помощью спец. функции `public static getFieldName = <T>(name: keyof T) => name;`. Делаем это чтобы жестко синхронизировать связку `ключ-модель`, иначе formly будет добавлять непонятные свойства в модель, и это все полетит на верх.
Пример:

```
    this.fields = [
      {
        key: Utils.getFieldName<ReleaseFormModel>('name'),
        type: 'input',
        className: 'col-6',
      ]
```

Эмитим модель только из `modelchange`, т.к она срабатывает только если пользователь меняет форму руками или меняются опции.
Перед эмитом клонируем модель с помощью `spread` или спец. библиотек, делаем защиту от дурака.
`ValueChange` - срабатывает чаще, это будет мешать в дебаге, лишними эмитами модели. В идеале модель должна эмититься только так как нам надо, например только если пользователь что-то меняет руками.
Пример:

```
  public onModelChange(model: ReleaseFormModel) {
    this.fdReleaseFormModelChange.emit({ data: { ...model }, status: this.formGroup.status as FORM_STATUS });
  }
```

При изменении опций формы, будет производится ее эмит. Почему не известно. Чтобы избежать этого делаем такой костыль:

```
  @Input() set isFormEnable(isEdit: boolean) {
    this._isFormEnable = isEdit;
    this.changeFormEnable(isEdit);
  }

  private changeFormEnable(isEnable: boolean): void {
    this.options.formState.disabled = !isEnable;
    const disableOptions = {
      onlySelf: true,
      emitEvent: false,
    };
    if (isEnable) {
      this.formGroup.enable(disableOptions);
      return;
    }
    this.formGroup.disable(disableOptions);
  }
```

Обязательно задаем собственный интерфейс для опций формы.
Затем данный интерфейс используем где он нужен, используем сильные стороны типизации `typescript` + `strict mode`
Пример:

```
interface ReleaseFormOptions extends FormlyFormOptions {
  formState: ReleaseFormState;
}

interface ReleaseFormState {
  disabled: boolean;
  minDate: moment.Moment;
}
  ......

 public options: ReleaseFormOptions = {
    formState: {
      disabled: true,
      minDate: moment(),
    },
  };
  .......
  expressionProperties: {
    'templateOptions.disabled': 'formState.disabled',
    'templateOptions.datepickerOptions.min': (release: ReleaseFormModel, releaseFormState: ReleaseFormState) => {
      return release.dateFrom ? release.dateFrom : releaseFormState.minDate;
    },
  },
```

Инициализируем опции, иначе при их выставлении в первый раз, сработает `onModelChange` формы

Внутри `expressionProperties` не возвращаем новые объекты, вместо этого берем их из аргументов, иначе Formly будет
бесконечно обновлять свою model и эмитить `valueChanges`.

Wrong code:

```
  'templateOptions.datepickerOptions.min': (release: ReleaseDTO, releaseFormState: ReleaseFormState) => {
    return release.dateFrom ? release.dateFrom : new Date();
  },
```

Nice code:

```
  'templateOptions.datepickerOptions.min': (release: ReleaseDTO, releaseFormState: ReleaseFormState) => {
    return release.dateFrom ? release.dateFrom : releaseFormState.minDate;
  }
```
