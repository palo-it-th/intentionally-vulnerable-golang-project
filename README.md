# Intentionally Vulnerable Golang Project

[![Run Dependency Check](https://github.com/gamertense/intentionally-vulnerable-golang-project/actions/workflows/dependency-check.yml/badge.svg)](https://github.com/gamertense/intentionally-vulnerable-golang-project/actions/workflows/dependency-check.yml)

This repository contains a minimal project designed to test Sonatype's `nancy` against an intentionally vulnerable list of dependencies. It also provides an example of how to use `nancy` in GitHub Actions.

## Running the Project Locally

To run the project locally, execute the following command:

```bash
go run main.go
```

You should see the following message in the console:

> HI I'M INTENTIONALLY USING VULNERABLE LIBS

## Running Dependency Check Locally

To run the dependency check locally, use the following command:

```bash
# Output the dependencies in JSON format and pipe it to the nancy container
go list -json -deps ./... | docker run --rm -i sonatypecommunity/nancy:latest sleuth
```

This command will display a summary table with the vulnerabilities found in the dependencies:

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Summary                     ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━┫
┃ Audited Dependencies    ┃ 3 ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━╋━━━┫
┃ Vulnerable Dependencies ┃ 2 ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━┻━━━┛
```

## Using GitHub Actions

This project includes a GitHub Actions workflow to automatically run the dependency check. The workflow is defined in the `.github/workflows/dependency-check.yml` file. The status of the latest run can be seen in the badge at the top of this README.

### Report format

To change the format of the report, modify the `nancyCommand` and `reportFile` variables in the workflow file. The following table shows the available formats:

| nancyCommand          | reportFile        |
| --------------------- | ----------------- |
| sleuth -o csv         | nancy-report.csv  |
| sleuth -o json-pretty | nancy-report.json |

### Downloading the report

To download the report from the GitHub Actions workflow, click on the `Run Dependency Check` badge and then select the latest run. In the `Artifacts` section, you will find the `nancy-report` file.
