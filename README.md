# M+Associati – Backend (ASP.NET API)

![C#](https://img.shields.io/badge/C%23-net8.0-blue)
![ASP.NET Core](https://img.shields.io/badge/ASP.NET%20Core-8.0-purple)
![Entity Framework](https://img.shields.io/badge/EF%20Core-8.0-green)
![SQL Server](https://img.shields.io/badge/Database-SQL%20Server-red)
![Swagger](https://img.shields.io/badge/Docs-Swagger%20%2F%20OpenAPI-brightgreen)
![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)

---

## 📌 Overview

**M+Associati Backend** is an ASP.NET Core 8 REST API that:

* Exposes CRUD endpoints for engineering **Projects**
* Persists data via **Entity Framework Core** on SQL Server
* Serves the M+Associati frontend web application
* Provides interactive API documentation via **Swagger / OpenAPI**
* Enforces **CORS** for controlled frontend access

---

## 🏗️ Architecture

```text
ASP.NET Core 8 Web API
        ↓
ProjectController (REST)
        ↓
IProjectRepository → ProjectRepository
        ↓
Entity Framework Core
        ↓
SQL Server
```

---

## 📁 Repository Structure

```text
mpiuassociati-backend/
│
└── api/
    ├── api.csproj
    ├── Program.cs
    ├── appsettings.json
    ├── appsettings.Development.json
    │
    ├── controller/
    │   └── ProjectController.cs
    │
    ├── data/
    │   └── ApplicationDBContext.cs
    │
    ├── models/
    │   └── Project.cs
    │
    ├── dtos/
    │   └── Project/
    │       ├── ProjectDto.cs
    │       ├── CreateProjectRequesDto.cs
    │       └── UpdateProjectRequestDto.cs
    │
    ├── interfaces/
    │   └── IProjectRepository.cs
    │
    ├── mappers/
    │   └── ProjectMappers.cs
    │
    ├── repository/
    │   └── ProjectRepository.cs
    │
    └── Migrations/
        └── 20240712090857_init.cs
```

---

## 📊 Data Model

### Project

| Field | Type | Description |
|-------|------|-------------|
| `Id` | int | Primary key |
| `ProjectName` | string | Project title |
| `ProjectDescription` | string | Full description |
| `ProjectPlace` | string | Location |
| `ProjectYear` | DateTime | Year of completion |
| `ProjectParentFilter` | string | Top-level category |
| `ProjectChildFilter` | string | Sub-category |
| `ProjectCover` | string | Cover image path |
| `ProjectImages` | List\<string\> | Gallery image paths |

---

## 🌐 API Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| `GET` | `/api/project` | Get all projects |
| `GET` | `/api/project/{id}` | Get project by ID |
| `POST` | `/api/project` | Create a new project |
| `PUT` | `/api/project/{id}` | Update a project |
| `DELETE` | `/api/project/{id}` | Delete a project |

---

## ⚙️ Configuration

File:

```
api/appsettings.json
```

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=<SERVER>;Database=<DB>;..."
  }
}
```

CORS is configured to allow:

```
https://localhost:44377
```

Update `Program.cs` to add production frontend origins.

---

## 🚀 Getting Started

### Prerequisites

* .NET 8 SDK
* SQL Server (local or remote)

### Run locally

```bash
cd api
dotnet restore
dotnet ef database update
dotnet run
```

Swagger UI available at:

```
https://localhost:<port>/swagger
```

---

## 🔄 Design Patterns

* **Repository pattern** – `IProjectRepository` / `ProjectRepository`
* **DTO mapping** – `ProjectMappers.cs` separates domain from transport layer
* **Dependency Injection** – All services registered in `Program.cs`

---

## 🔒 Security

* CORS policy restricts allowed origins
* HTTPS redirection enforced
* No secrets in source code – use environment variables or `appsettings.local.json`

---

## 🚀 Roadmap

* JWT authentication
* Pagination & filtering on GET endpoints
* Azure deployment (App Service + Azure SQL)
* Unit & integration tests

---

## 📄 License

© 2026 - Andrea Magnaghi

---

## 👨‍💻 Version

```
1.0.0
```
