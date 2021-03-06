# [part](https://github.com/MediaMath/part) &middot; [![CircleCI Status](https://circleci.com/gh/MediaMath/part.svg?style=shield)](https://circleci.com/gh/MediaMath/part) [![GitHub license](https://img.shields.io/badge/license-BSD3-blue.svg)](https://github.com/MediaMath/part/blob/master/LICENSE) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/MediaMath/part/blob/master/CONTRIBUTING.md)

# part
Publish to artifactory as a cli

## What it does

Part is a simple cli that take some command line parameters (part -h for documentation) and an artifact (zip, jar, etc).  It then creates a maven pom and publishes it and the artifact to artifactory.  This allows for easy publishing of artifacts that can be found via Maven GAVC (Group, Artifact, Version, Classifier) style searches via the artifactory rest api.  See the [maven pom reference](https://maven.apache.org/pom.html) for more details about gavc coordinates generally and the [artifactory rest documentation](https://www.jfrog.com/confluence/display/RTF/Artifactory+REST+API#ArtifactoryRESTAPI-GAVCSearch) for artifactory GAVC searches.

## Installation

If you are using this as part of a golang build process, just install via standard go tools:

```bash
go install -a github.com/MediaMath/part
```

Otherwise you can download the latest zip package of it:

```bash
wget https://artifactory.mediamath.com/artifactory/libs-release-global/com/mediamath/part/[RELEASE]/part-[RELEASE].zip
```

## Artifactory REST API endpoint

The artifactory rest api endpoint must be provided either on the command line via the -h flag or via the ARTIFACTORY_HOST parameter.  This should be the fully formed REST API endpoint, not just the host domain. (e.g. https://artifactory.mediamath.com/artifactory).

## Artifactory Authentication

Part allows for the publishing to artifactory via basic auth via one of the following 3 mechanisms.

### JSON File

If a filename is passed in via the -credentials flag with the .json file extension, it will be parsed as a json object expected to be of the form: 

```json
{ 
	"user":"username", 
	"password":"password"
}
```

### INI File

If a filename is passed in via the -credentials flag without the .json file extension, it will be parsed as a limited ini file of the form: 

```ini
user=username
password=password
```

### Environment Variables

If no filename is passed in via the -credentials flag part will look for the ARTIFACTORY_USER and ARTIFACTORY_PASSWORD environment variables for authentication.

### No Auth

If no filename is passed and both environment variables are not provided, part will attempt to publish without authentication.
