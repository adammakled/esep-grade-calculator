# ESEP Grade Calculator

This library is a simple utility to calculate your grades. It is written in Go and has no
dependencies outside of the standard library.

A student can have three kinds of grades: assignments, exams, and essays. The calculator
averages each kind, weights the averages (assignments 50%, exams 35%, essays 15%), and
converts the result into a letter grade:

| Score    | Letter |
|----------|--------|
| 90+      | A      |
| 80 - 89  | B      |
| 70 - 79  | C      |
| 60 - 69  | D      |
| below 60 | F      |

## Requirements

Go 1.24 or newer. You can check your version with:
```
go version
```
If you don't have it, download it from https://go.dev/dl/ (or `brew install go` on macOS).

## Project layout

```
README.MD
grade-calculator/
    go.mod                      module definition (module name and Go version)
    grade_calculator.go         the GradeCalculator library code
    grade_calculator_test.go    unit tests
```

Note that the Go code lives in the `grade-calculator/` folder (with a dash), so all `go`
commands need to be run from inside that folder.

## Setup

```
git clone https://github.com/adammakled/esep-grade-calculator.git
cd esep-grade-calculator/grade-calculator
```

## Usage

The package is named `esepunittests`. Create a calculator, add grades, then ask for the final grade:

```go
gc := NewGradeCalculator()

gc.AddGrade("open source assignment", 100, Assignment)
gc.AddGrade("exam 1", 95, Exam)
gc.AddGrade("essay on ai ethics", 91, Essay)

letter := gc.GetFinalGrade() // "A"
```

The grade type has to be one of `Assignment`, `Exam`, or `Essay`.

## Running the tests

From inside `grade-calculator/`:
```
go test ./...
```

Add `-v` to see each test by name:
```
go test -v ./...
```

## Code coverage

Print the coverage percentage:
```
go test -cover ./...
```

Write a coverage profile and look at it line by line:
```
go test -coverprofile=coverage.txt ./...
go tool cover -func=coverage.txt     # coverage per function
go tool cover -html=coverage.txt     # opens a browser view, uncovered lines are red
```

## Known issues

When this repo was handed over, `TestGetGradeA` and `TestGetGradeB` fail and coverage is 80%.
See the tests and `calculateNumericalGrade` / `computeAverage` in `grade_calculator.go`.
