# Using the API

EventCalendar is shipped with an API that you can leverage for custom queries on the saved calendar, event, locations and organiser. Also it provides methods to create, update and delete entities related to the package.

The package API is build following the CQRS principal to seperate writes from reads. For every write you need the build in CommandDispatcher using the build in commands, or the build in QueryDispatcher using the build in queries.

The package also uses Ninject for dependency injection. That way you only work with the interfaces not with the actual implementation. To get the implementation the EventCalendarServiceContainer can be used.

Sample:
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
    <p>
```csharp
var allCalendarResult = _queryDispatcher.Dispatch<GetAllCalendarQuery, GetAllCalendarQueryResult>(new GetAllCalendarQuery());
```
    </p>
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    <p>
```csharp
var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });
```
    </p>
</details>

<details>
    <summary>GetCalendarByIdQuery</summary>
    <p>
```csharp
var calendarByIdResult = _queryDispatcher.Dispatch<GetCalendarByIdQuery, GetCalendarByIdQueryResult>(new GetCalendarByIdQuery { CalendarId = id });
```
    </p>
</details>

<details>
    <summary>GetPagedCalendarQuery</summary>
    <p>
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
    </p>
</details>

<details>
    <summary>GetIcsForCalendarQuery</summary>
    <p>
```csharp
var result = dispatcher.Dispatch<GetIcsForCalendarQuery, GetIcsForCalendarQueryResult>(new GetIcsForCalendarQuery { CalendarId = id, Culture = CultureInfo.CurrentCulture.ToString() });
```
    </p>
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    <p>
```var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });```
    </p>
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    <p>
```var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });```
    </p>
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    <p>
```var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });```
    </p>
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    <p>
```var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });```
    </p>
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    <p>
```var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });```
    </p>
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    <p>
```var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });```
    </p>
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    <p>
```var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });```
    </p>
</details>

<details>
    <summary>GetAllCalendarByUserQuery</summary>
    <p>
```var calendarResult = _queryDispatcher.Dispatch<GetAllCalendarByUserQuery, GetAllCalendarByUserQueryResult>(new GetAllCalendarByUserQuery() { UserId = _user.Id });```
    </p>
</details>