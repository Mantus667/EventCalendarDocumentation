# Using the API

EventCalendar is shipped with an API that you can leverage for custom queries on the saved calendar, event, locations and organiser. Also it provides methods to create, update and delete entities related to the package.

The package API is build following the CQRS principal to seperate writes from reads. For every write you need the build in CommandDispatcher using the build in commands, or the build in QueryDispatcher using the build in queries.

The package also uses Ninject for dependency injection. That way you only work with the interfaces not with the actual implementation. To get the implementation the EventCalendarServiceContainer can be used.

__Sample:__

```csharp
EventCalendarServiceContainer.GetService<ICommandDispatcher>();
```

## Fetching data

Data can be fetched by using one of the multiple queries build in. The queries are executed by the IQueryDispatcher using the proper QueryHandler and returning an IQueryResult implementation. So every query consists of three classes:

1. Query implementation inheriting from ```IQuery``` interface
2. QueryHandler implementation inheriting from ```IQueryHandler<TParameter, TResult> where TResult : IQueryResult where TParameter : IQuery```
3. QueryResult inheriting from ```IQueryResult```

Following the list of currently available queries with an example implementation:

<details>
    <summary>GetAllCalendarQuery</summary>

```csharp

var allCalendarResult = _queryDispatcher.Dispatch<GetAllCalendarQuery, GetAllCalendarQueryResult>(new GetAllCalendarQuery());

```
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>

```csharp

var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });

```
</details>

<details>
    <summary>GetCalendarByIdQuery</summary>
    
```csharp
var calendarByIdResult = _queryDispatcher.Dispatch<GetCalendarByIdQuery, GetCalendarByIdQueryResult>(new GetCalendarByIdQuery { CalendarId = id });
```
    
</details>

<details>
    <summary>GetPagedCalendarQuery</summary>
    
```csharp
var pagedCalendarQuery = new GetPagedCalendarQuery()
    {
        itemsPerPage = itemsPerPage,
        pageNumber = pageNumber,
        sortColumn = sortColumn,
        sortOrder = sortOrder,
        searchTerm = searchTerm,
        UserId = Security.CurrentUser.Id
    };
    var pagedCalendarResult = _queryDispatcher.Dispatch<GetPagedCalendarQuery, GetPagedCalendarQueryResult>(pagedCalendarQuery);
```
    
</details>

<details>
    <summary>GetIcsForCalendarQuery</summary>
    
```csharp
var result = dispatcher.Dispatch<GetIcsForCalendarQuery, GetIcsForCalendarQueryResult>(new GetIcsForCalendarQuery { CalendarId = id, Culture = CultureInfo.CurrentCulture.ToString() });
```
    
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    
```csharp
var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });
```
    
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    
```csharp
var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });
```
    
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    
```csharp
var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });
```
    
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    
```csharp
var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });
```
    
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    
```csharp
var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });
```
    
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    
```csharp
var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });
```
    
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    
```csharp
var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });
```
    
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    
```csharp
var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });
```
    
</details>

## Adding data

The package uses commands for write actions like adding new entities or updating them. Commands are executed by the ICommandDispatcher using the proper CommandHandler and returning a CommandResult. So every command consists of three classes:

1. Command implementation inheriting from ```ICommand``` interface
2. CommandHandler implementation inheriting from ```ICommandyHandler<in TParameter> where TParameter : ICommand```
3. CommandResult class

The CommandResult class provides the following properties:
```csharp
public bool Success { get; set; }

public string Message { get; set; }

public object Data { get; set; }

public Exception Exception { get; set; }
```

It returns the entitie which was used in the Command, an indicator of the command was successfull, an additional message and the exception if something went wrong during command execution.

Following the list of currently available commands with an example implementation:

<details>
    <summary>AddCalendarCommand</summary>
    
```csharp

var commandResult = _commandDispatcher.Dispatch<AddCalendarCommand>(new AddCalendarCommand() { Calendar = calendar });
```
    
</details>

<details>
    <summary>AddCalendarToUserCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<AddCalendarToUserCommand>(new AddCalendarToUserCommand() { UserId = userId, Calendar = calendar });
```
    
</details>

<details>
    <summary>UpdateCalendarCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<UpdateCalendarCommand>(new UpdateCalendarCommand() { Calendar = calendar });
```
    
</details>

<details>
    <summary>DeleteCalendarByIdCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<DeleteCalendarByIdCommand>(new DeleteCalendarByIdCommand() { CalendarId = calendarId });
```
    
</details>

<details>
    <summary>AddEventCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<AddEventCommand>(new AddEventCommand() { Event = event });
```
    
</details>

<details>
    <summary>UpdateEventCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<UpdateEventCommand>(new UpdateEventCommand() { Event = event });
```
    
</details>

<details>
    <summary>DeleteEventByIdCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<DeleteEventByIdCommand>(new DeleteEventByIdCommand() { EventId = eventId });
```
    
</details>

<details>
    <summary>AddLocationCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<AddLocationCommand>(new AddLocationCommand() { Location = location });
```
    
</details>

<details>
    <summary>AddLocationToUserCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<AddLocationToUserCommand>(new AddLocationToUserCommand() { UserId = userId, Location = location });
```
    
</details>

<details>
    <summary>UpdateLocationCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<UpdateLocationCommand>(new UpdateLocationCommand() { Location = location });
```
    
</details>

<details>
    <summary>DeleteLocationByIdCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<DeleteLocationByIdCommand>(new DeleteLocationByIdCommand() { LocationId = locationId });
```
    
</details>

<details>
    <summary>AddOrganiserCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<AddOrganiserCommand>(new AddOrganiserCommand() { Organiser = organiser });
```
    
</details>

<details>
    <summary>AddOrganiserToUserCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<AddOrganiserToUserCommand>(new AddOrganiserToUserCommand() { UserId = userId, Organiser = organiser });
```
    
</details>

<details>
    <summary>UpdateOrganiserCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<UpdateOrganiserCommand>(new UpdateOrganiserCommand() { Organiser = organiser });
```
    
</details>

<details>
    <summary>DeleteOrganiserByIdCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<DeleteOrganiserByIdCommand>(new DeleteOrganiserByIdCommand() { OrganiserId = organiserId });
```
    
</details>

<details>
    <summary>AddNewUserIfNotExistsCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<AddNewUserIfNotExistsCommand>(new AddNewUserIfNotExistsCommand() { User = user });
```
    
</details>

<details>
    <summary>UpdateUserCommand</summary>
    
```csharp

var commandResult = _commandDispatcher.Dispatch<UpdateUserCommand>(new UpdateUserCommand() { User = user });

```
    
</details>

<details>
    <summary>ImportIcsFilesCommand</summary>
    
```csharp
var commandResult = _commandDispatcher.Dispatch<ImportIcsFilesCommand>(new ImportIcsFilesCommand() { FileNames = fileNames, CalendarId = calendarId });
```
    
</details>

### Validating commands

The package provides the possibility to validate commands before they are executed. For this implementations of ```IValidationHandler<in TParameter> where TParameter : ICommand``` are used.
Each validation handler can be registered for a specific command and is executed before executing the actual command. The handler returns a CommandValidationResult which indicates the state of the validation.