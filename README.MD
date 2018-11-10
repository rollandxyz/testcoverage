
# Collecting test coverage using Coverlet and SonarQube for a .net core project

sudo docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

sudo apt install default-jdk

dotnet test calculation.tests/calculation.tests.csproj /p:CollectCoverage=true /p:CoverletOutputFormat=opencover
dotnet build-server shutdown
dotnet sonarscanner begin /k:"calculation" /d:sonar.host.url=http://localhost:9000 /d:sonar.cs.opencover.reportsPaths="calculation.tests\coverage.opencover.xml" /d:sonar.coverage.exclusions="**Tests*.cs"
dotnet build
dotnet sonarscanner end


## reference
https://medium.com/agilix/collecting-test-coverage-using-coverlet-and-sonarqube-for-a-net-core-project-ef4a507d4b28

https://github.com/merken/testcoverage

