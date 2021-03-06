SonarQube plugin for Groovy
==========

## /!\ This plugin is looking for a maintainer
If you are interested, please ask on SonarQube user group.

### Build status

[![Build Status](https://api.travis-ci.org/SonarQubeCommunity/sonar-groovy.png)](https://travis-ci.org/SonarQubeCommunity/sonar-groovy)

## Description
The plugin enables analysis of Groovy within SonarQube.

It leverages [CodeNarc](http://codenarc.sourceforge.net/) to raise issues against coding rules, [GMetrics](http://gmetrics.sourceforge.net/) for cyclomatic complexity and [Cobertura](http://cobertura.sourceforge.net/) or [JaCoCo](http://www.eclemma.org/jacoco/) for code coverage.

Plugin   | 0.1 | 0.2 | 0.3  | 0.4  | 0.5    | 0.6  | 1.0  | 1.1  | 1.1.1 | 1.2  | 1.3    | 1.3.1  | 1.4
---------|-----|-----|------|------|--------|------|------|------|-------|------|--------|--------|-------
CodeNarc | 0.9 | 0.9 | 0.13 | 0.15 | 0.16.1 | 0.17 | 0.20 | 0.23 | 0.23  | 0.24 | 0.24.1 | 0.24.1 | 0.25.2
GMetrics | 0.2 | 0.2 | 0.3  | 0.3  | 0.4    | 0.5  | 0.6  | 0.6  | 0.7   | 0.7  | 0.7    | 0.7    | 0.7

## Steps to Analyze a Groovy Project
1. Install SonarQube Server
1. Install SonarQube Scanner and be sure you can call `sonar-scanner` from the directory where you have your source code
1. Install the Groovy Plugin.
1. Create a _sonar-project.properties_ file at the root of your project
1. Run `sonar-scanner` command from the project root dir
1. Follow the link provided at the end of the analysis to browse your project's quality in SonarQube UI

## Notes
*CodeNarc*
It is possible to reuse a previously generated report from CodeNarc by setting the `sonar.groovy.codenarc.reportPath` property.

*Groovy File Suffixes*
It is possible to define multiple groovy file suffixes to be recognized by setting the `sonar.groovy.file.suffixes` property. Note that by default, only files having `.groovy` as extension will be analyzed.

*Unit Tests Execution Reports*
Import unit tests execution reports (JUnit XML format) by setting the sonar.junit.reportsPath property. Default location is _target/surefire-reports_.

*JaCoCo and Binaries*
The groovy plugin requires access to source binaries when analyzing JaCoCo reports. Consequently, property `sonar.groovy.binaries` has to be configured for the analysis (comma-separated paths to binary folders). For Maven and gradle projects, the property is automatically set.

## Coverage Results Import
The Groovy Plugin does not generate its own test coverage report, but re-uses the ones generated by Cobertura or JaCoCo. 

### Code Coverage with Cobertura
To display code coverage data:

1. Prior to the SonarQube analysis, execute your unit tests and generate the Cobertura XML report.
1. Import this report while running the SonarQube analysis by setting the `sonar.groovy.cobertura.reportPath` property to the path to the Cobertura XML report. The path may be absolute or relative to the project base directory.

### Code Coverage with JaCoCo
To display code coverage data:

1. Prior to the SonarQube analysis, execute your tests and generate the JaCoCo exec file(s).
1. In order to be able to read the exec report file, and as JaCoCo bases its analysis on binaries, set the sonar.binaries property.
1. Set the `sonar.groovy.jacoco.reportPath` property to the path to the JaCoCo exec file related to your unit tests.
1. (Optional) If you are running integration tests on top of your unit tests, you may want to set the `sonar.groovy.jacoco.itReportPath` to the path to JaCoCo exec file related to the integration tests.
1. Run the SonarQube analysis.
