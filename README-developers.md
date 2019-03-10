# README for developers

## Development
Compile all C# projects (this will also install all the dependencies):
```
./tasks build
# OR:
dotnet build
```

Run C# tests:
```
./tasks test
# OR:
dotnet test
```

Run integration tests with [Bats](https://github.com/sstephenson/bats):
```
./tasks itest
```

### Install Bats on Linux
```
git clone --depth 1 https://github.com/sstephenson/bats.git /opt/bats
git clone --depth 1 https://github.com/ztombol/bats-support.git /opt/bats-support
git clone --depth 1 https://github.com/ztombol/bats-assert.git /opt/bats-assert
/opt/bats/install.sh /usr/local
```

## How the C# solution was set up
```
# Create a C# .sln file (solution)
work$ dotnet new sln --name Backend

# Create a C# project of type Console (CLI application)
work$ mkdir -p src/BackendConsole
work$ cd src/BackendConsole
work/src/BackendConsole$ dotnet new console
work/src/BackendConsole$ cd ../..

# Reference the console C# project from the .sln file
work$ dotnet sln ./Backend.sln add ./src/BackendConsole/BackendConsole.csproj

# Create a C# project with tests
work$ mkdir -p tests/BackendConsole.Tests
work$ cd tests/BackendConsole.Tests
work/tests/BackendConsole.Tests$ dotnet new xunit
work/tests/BackendConsole.Tests$ cd ../..

# Reference the tests C# project from the .sln file
work$ dotnet sln ./Backend.sln add tests/BackendConsole.Tests/BackendConsole.Tests.csproj

# Reference the console C# project from the tests C# project
work$ dotnet add tests/BackendConsole.Tests/BackendConsole.Tests.csproj reference src/BackendConsole/BackendConsole.csproj
```

## How external dependencies were added
Add external packages references to the C# projects files
```
work$ dotnet add src/BackendConsole/ package --version=2.1.2 Npgsql.EntityFrameworkCore.PostgreSQL
work$ dotnet add src/BackendConsole/ package Microsoft.EntityFrameworkCore.Design
```
