# Scan Monster Usage Guide

## Summary

Scan Monster is a powerful automation tool for initiating scans on multiple repositories using the Checkmarx One APIs. It supports several types of scans, including SAST, SCA, IaC, and API, with the flexibility to specify scan presets and intervals between scans. Designed for ad hoc scan operations, it simplifies bulk vulnerability assessments across codebases.


## Syntax and Arguments

Execute the script using the following command line:

```bash
python scan_monster.py --base_url BASE_URL --tenant_name TENANT_NAME --api_key API_KEY --repo_file REPO_FILE [OPTIONS]
```

### Required Arguments

- `--base_url`: The base URL of the Checkmarx One region.
- `--tenant_name`: Your tenant name in Checkmarx One.
- `--api_key`: Your API key for authenticating with the Checkmarx One APIs.
- `--repo_file`: Path to a file containing a list of repository URLs to scan.

### Optional Arguments

- `--iam_base_url`: Optional IAM base URL. Defaults to the same as `base_url` if not provided.
- `--github_token`: Personal access token for GitHub repositories.
- `--gitlab_token`: Personal access token for GitLab repositories.
- `--bitbucket_token`: Personal access token for Bitbucket repositories.
- `--azure_token`: Personal access token for Azure DevOps repositories.
- `--sast [SAST_PRESET]`: Enable SAST scan with an optional preset name.
- `--sca`: Enable SCA scan. (Flag, no value required)
- `--iac`: Enable IaC scan. (Flag, no value required)
- `--api`: Enable API scan. (Flag, no value required)
- `--threads THREADS`: Maximum number of threads to use for scan initiation.
- `--debug`: Enable debug output. (Flag, no value required)


## Prerequisites

 1. Python. [Install python](https://www.python.org/downloads/)

 2. Dependencies. Install all necessary's dependencies for the scan_monster.py script on the machine that will be running the
       tool. 
       See the scan_monster.py file for a list of `imports`

	example:
`$ pip install requests`

 3. Repos. You need a list of repos to scan. Edit the included
       repos.txt file that has the repos you want to scan listed line by
       line in plain text.

	example:
`https://github.com/appsecco/dvja`

  


## Usage Examples

Initiate all types of scans on repositories listed in the file:

```bash
python scan_monster.py --base_url https://cxone.example.com --tenant_name mytenant --api_key 12345 --repo_file repos.txt
```

Initiate SAST and SCA scans with a preset for SAST:

```bash
python scan_monster.py --base_url https://cxone.example.com --tenant_name mytenant --api_key 12345 --repo_file repos.txt --sast "MyCustomPreset" --sca
```

Initiate scans with a waiting period of 5 minutes between each scan:

```bash
python scan_monster.py --base_url https://cxone.example.com --tenant_name mytenant --api_key 12345 --repo_file repos.txt --space_scans 5
```

Initiate scans with debug output:

```bash
python scan_monster.py --base_url https://cxone.example.com --tenant_name mytenant --api_key 12345 --repo_file repos.txt --debug
```

## Output

Scan Monster will output the status of each scan initiation and any errors encountered during the process. If debug mode is enabled, it will provide detailed information about the scan configurations and the response from the Checkmarx One APIs.

## Docker Container Setup
To run Scan Monster in a Docker container, follow these steps:

### Building the Docker Image
Ensure Docker is installed on your machine. Install Docker.

Navigate to the directory containing the Dockerfile and run the following command to build the Docker image:

```bash
docker build -t scan-monster-image .
```
This command creates a Docker image named scan-monster-image.

### Running the Docker Container
Use the following command to run the Scan Monster tool inside a Docker container:

```bash

docker run -v <path-to-repos-folder>:/app/ scan-monster-image --base_url <BASE_URL> --tenant_name <TENANT_NAME> --api_key <API_KEY> --repo_file /app/<repos-file> [OPTIONS]
```

## License

MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
