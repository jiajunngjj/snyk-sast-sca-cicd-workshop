# Snyk Code, Snyk Open Source and CI/CD Workshop

A hands-on session to see how you can implement Snyk Code and Snyk Open Source early, to easily find and fix both security issues in their own proprietary code as well as known vulnerabilities in their open source dependencies, reducing risk and accelerate the software development.

## Prerequisites

* public GitHub account - http://github.com
* git CLI - https://git-scm.com/downloads
* snyk CLI - https://support.snyk.io/hc/en-us/articles/360003812538-Install-the-Snyk-CLI
* Registered account on Snyk App - http://app.snyk.io

## Tasks

In this hands-on workshop we will achieve the following:

* [Step 1 - Fork the highly vulnerable Juice-Shop Application](#step-1---fork-the-highly-vulnerable-juice-shop-application)
* [Step 2 - Configure GitHub Integration](#step-2---configure-github-integration)

Snyk Code steps

* [Step 3 - Enable Snyk Code within Snyk App](#step-3---enable-snyk-code-within-snyk-app)
* [Step 4 - Add project to find Snyk Code Vulnerabilities](#step-4---add-project-to-find-snyk-code-vulnerabilities)
* [Step 5 - Run a Snyk Code CLI Test](#step-5---run-a-snyk-code-cli-test)

Snyk Open Source steps

* [Step 6 - Find vulnerabilities](#step-6---find-vulnerabilities)
* [Step 7 - Fix using a Pull Request](#step-7---fix-using-a-pull-request)
* [Step 8 - Run a Snyk CLI Test](#step-8---run-a-snyk-cli-test)

Set up GitHub Actions to run Snyk Code and Snyk Open Source
* [Step 9 - Retrieve the Snyk API token from Snyk App](#step-9---retrieve-the-snyk-api-token-from-snyk-app)
* [Step 10 - Add the Snyk API token into the GitHub repository secret](#step-10---add-the-snyk-api-token-into-the-github-repository-secret)
* [Step 11 - Create the GitHub Actions workflow](#step-11---create-the-github-actions-workflow)

# Workshop Steps

_NOTE_: It is assumed your using a mac for these steps, but it should also work on Windows or linux with some modifications to the scripts potentially.

## Step 1 - Fork the highly vulnerable Juice-Shop Application

_NOTE: You may have already forked the Juice-Shop application in that case go ahead and skip this step_

Navigate to the following GitHub repo - https://github.com/juice-shop/juice-shop

_NOTE: this repo comes from the project Juice Shop from OWASP_

* Click on the "**Fork**" button
* Ensure you are forking this repo to your public GitHub account
* Click done

![juice_shop_screenshot](https://user-images.githubusercontent.com/25560159/194021463-b8dcfbd5-2c35-4944-abec-86731997c3ab.png)

## Step 2 - Configure GitHub Integration

_NOTE: You may have already setup GitHub integration in that case go ahead and skip this step_

First we need to connect Snyk to GitHub so we can import our Repository. Do so by following these steps below:

* Login to http://app.snyk.io Sign up if you haven't already.
* Navigating to **Integrations** -> **Source Control** -> **GitHub**
* Fill in your Account Credentials to Connect your GitHub Account.

![integration workshop](https://user-images.githubusercontent.com/25560159/194023826-1cb8242f-0bc3-4776-8fd3-9b99cb723b87.png)

# Snyk Code Steps

Snyk Code is developer-first, embedding SAST as part of the development process, enabling developers to build software securely during development, not trying to find and fix problems after the code is compiled. Snyk Code works in the IDEs and SCMs developers use to build and review software and provides fast, actionable, meaningful results to fix issues in real-time

## Step 3 - Enable Snyk Code within Snyk App

* Click on the "**Settings**" button on the top most navigation bar as shown below

![setting_screenshot](https://user-images.githubusercontent.com/25560159/194026233-ad7352b8-e00e-447d-8c27-e5601f4ceacd.png)

* Click on "**Snyk Code**", then enable it and click "**Save Changes**" as shown below

![snyk_code_setting](https://user-images.githubusercontent.com/25560159/194027538-f121e536-f1a3-4e04-9124-f9326a33cbfc.png)

## Step 4 - Add project to find Snyk Code Vulnerabilities

Now that Snyk is connected to your GitHub Account, import the Forked Repo "**juice-shop**" into Snyk as a Project.

* Navigate to Projects
* Click "**Add Project**" then select "**GitHub**"
* Click on the Repo you forked "**juice-shop**"
* Click "**Add Selected Repositories**"

![alt tag](https://user-images.githubusercontent.com/25560159/194028382-cd12cc2c-aa2f-4cab-bc2f-d6525dee9099.png)

* Once complete you should see a "**Code Analysis**" project as shown below

![alt tag](https://user-images.githubusercontent.com/25560159/194032242-16b89a55-b96a-4137-91e9-4fe2a21ec52b.png)

* Click on "**Code Analysis**" to view our SAST scan results

For each Vulnerability, Snyk displays the following:

1. Each Vulnerability grouped by severity
2. Each Vulnerability links to the CWE category code
3. Each Vulnerability shows the CWE category name
4. Displays the line of code where the security issue exists
5. Description for the issue and the code file name it exists in
6. A link to a Snyk Learn module on how to fix these type of vulnerabilities if available
7. The ability to ignore issues you wish to remove from the list

![alt tag](https://i.ibb.co/yk83tyP/Snyk-Code-vuln.png)

* Click on the "**Full Details**" button as shown below

Snyk products all provide a developer-friendly experience, so Snyk Code helps developers to quickly understand the problem, learn the background, and how to approach it. Snyk Code helps you understand the dangerous code flow step-by-step. For every issue, Code also provides a link to the lines in the relevant files, to view more details on the problem like the CWE, and how to approach it.

![alt tag](https://i.ibb.co/HnL22t7/Cross-site-scripting-Dataflow.png)

* Click on "**Fix Analysis**" to see how you can fix the issue based on other open source project. On this page you get not just source code example fixes but also the following detailed information

1. Details
2. Types Of Attacks
3. Affected Environments
4. How to prevent

![alt tag](https://i.ibb.co/M21xScH/Cross-site-scripting-Fix-Analysis.png)

## Step 5 - Run a Snyk Code CLI Test

In addition to the Snyk App UI we also have, snyk - CLI a build-time tool to find & fix known vulnerabilities in open-source dependencies, IaC configuration files and SAST scans on the source code files itself (Snyk Code).

* Before we get started please make sure you have setup the Snyk CLI. There are various install options as per the links below. Using the prebuilt binaries means you don't have to install NPM to install the Snyk CLI.

1. Install Page - https://support.snyk.io/hc/en-us/articles/360003812538-Install-the-Snyk-CLI
2. Prebuilt Binaries - https://github.com/snyk/snyk/releases

_Note: Please ensure you have the latest version of the Snyk CLI installed a version equal to or greater than the version below_

```bash
$ snyk --version
1.801.0
```

* Authorize the Snyk CLI with your account as follows

```bash
$ snyk auth

Now redirecting you to our auth page, go ahead and log in,
and once the auth is complete, return to this prompt and you'll
be ready to start using snyk.

If you can't wait use this url:
https://snyk.io/login?token=ff75a099-4a9f-4b3d-b75c-bf9847672e9c&utm_medium=cli&utm_source=cli&utm_campaign=cli&os=darwin&docker=false

Your account has been authenticated. Snyk is now ready to be used.
```

* Clone your forked repository as shown below. You can use your own GitHub forked repo here instead of the one shown below if you like

```shell
$ git clone https://github.com/jiajunngjj/juice-shop
Cloning into 'juice-shop'...
remote: Enumerating objects: 94967, done.
remote: Counting objects: 100% (17/17), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 94967 (delta 5), reused 13 (delta 4), pack-reused 94950
Receiving objects: 100% (94967/94967), 157.66 MiB | 10.35 MiB/s, done.
Resolving deltas: 100% (72676/72676), done.
```

* Change to the "**juice-shop**" directory

```shell
$ cd juice-shop
```

* At this point let's go ahead and run our first "**snyk code test**" as shown below

```shell
$ snyk code test

Testing /Users/jiajun/workspace/github/juice-shop ...

 ✗ [Low] Cleartext Transmission of Sensitive Information
     Path: test/e2eSubfolder.js, line 7
     Info: http (used in require) is an insecure protocol and should not be used in new code.

 ✗ [Low] Cleartext Transmission of Sensitive Information
     Path: test/api/productReviewApiSpec.js, line 9
     Info: http (used in require) is an insecure protocol and should not be used in new code.

...

 ✗ [High] Server-Side Request Forgery (SSRF)
     Path: routes/profileImageUrlUpload.js, line 19
     Info: Unsanitized input from the HTTP request body flows into request.get, where it is used as an URL to perform a request. This may result in a Server-Side Request Forgery vulnerability.

 ✗ [High] Server-Side Request Forgery (SSRF)
     Path: frontend/src/app/Services/configuration.service.ts, line 111
     Info: Unsanitized input from data from a remote resource flows into get, where it is used as an URL to perform a request. This may result in a Server-Side Request Forgery vulnerability.

 ✗ [High] Improper Neutralization of Directives in Statically Saved Code
     Path: routes/userProfile.js, line 46
     Info: Unsanitized input from cookies flows into pug.compile, where it is used to construct a template that gets rendered. This may result in a Server-Side Template Injection vulnerability.


✔ Test completed

Organization:      jj.ng
Test type:         Static code analysis
Project path:      /Users/jiajun/workspace/github/juice-shop

267 Code issues found
28 [High]   86 [Medium]   153 [Low

```

# Snyk Open Source Steps

Snyk Open Source is a Software Composition Analysis took which seamlessly and proactively finds, prioritizes and fixes vulnerabilities and license violations in open source dependencies

## Step 6 - Find vulnerabilities

* Since Juice-Shop project had been imported in the Step 3, you should see multiple "**package.json**" projects as shown below.

![snyk_open_source](https://user-images.githubusercontent.com/25560159/194291603-cd7aa623-adc6-4cb8-a66b-83c20c55cc43.png)

* Click on the second "**package.json**" to view our Open Source scan results

First let's explore the Juice-Shop project risks by clicking on the "**package.json**" file which is the manifest file where the open source dependencies are declared.

![alt tag](https://i.ibb.co/ZhN6tXY/Package-json-view.png)

Thenk go back on the Snyk WebUI and let's have a look at the vulnerabilities.

For each Vulnerability, Snyk displays the following ordered by our [Proprietary Priority Score](https://docs.snyk.io/features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score) :
1. The module that introduced it and, in the case of transitive dependencies, its direct dependency,
1. Details on the path and proposed Remediation, as well as the specific vulnerable functions
1. Overview
1. Exploit maturity
1. Links to CWE, CVE and CVSS Score
1. Plus more ...

![alt tag](https://i.ibb.co/xq2GWCs/Snyk-OS-vuln.png)

## Step 7 - Fix using a Pull Request

When using the GitHub integration, and if a fix is available, Snyk can automatically upgrade the vulnerable dependency to a non-vulnerable version through a Pull Request.

* Click on "**Fix this vulnerability**" for "**Prototype Pollution**" issue as shown below

![alt tag](https://i.ibb.co/9NHPmn2/Snyk-OS-Fix-this-vuln.png)

* On the next screen, you'll be able to confirm the issue to fix with this PR. Click "**Open a Fix PR**"

![alt tag](https://user-images.githubusercontent.com/25560159/194293540-a854d9d6-4220-465f-9d49-a97534a84b3e.png)
![alt tag](https://i.ibb.co/p2Lx5Rd/Open-fix-pr-button.png)

* Once it's ready, you'll be taken to the PR in GitHub, where you can review the changes in the file diff view:

Snyk integrates with your preferred Git repository to scan your manifest files for any new code and potential vulnerabilities whenever you submit a pull request (PR), protecting the security of your code before you ever merge it with the main branch

![alt tag](https://user-images.githubusercontent.com/25560159/194295151-e8204fca-d2fd-40cd-a87d-2cc9bc6ea4aa.png)

* We see that CI checks completed successfully, assuring us we didn't introduce a breaking change

![alt tag](https://user-images.githubusercontent.com/25560159/194295380-54dabfbd-1997-4afa-9243-1b416118f82d.png)

* Optionally now, go ahead and merge the PR!
* Back in Snyk we can appreciate that our package.json file has 1 less Critical Severity Vulnerability if you did fix it

### Step 8 - Run a Snyk CLI Test

In addition to the Snyk App UI we also have, snyk - CLI and build-time tool to find & fix known vulnerabilities in open-source dependencies. The CLI is what is used in DevOps pipelines to introduce Application Security Scans as part of that workflow to push applications into production.

* Before we get started please make sure you have setup the Snyk CLI. There are various install options as per the links below. Using the prebuilt binaries means you don't have to install NPM to install the Snyk CLI.

1. Install Page - https://support.snyk.io/hc/en-us/articles/360003812538-Install-the-Snyk-CLI
1. Prebuilt Binaries - https://github.com/snyk/snyk/releases

* In order to run a Snyk CLI test we must install the npm packages so if you have npm in your path you can install them as follows

Check your Node version:

```shell
$ node -v
```

_Note_: If you're using Node version v14.x or v16.x or v18.x, you can proceed to the next step (npm install), else please set up Node version 14 (Juice-Shop supported compatibility)

For MacOS brew user:
```shell
$ brew install node@14
$ export PATH="/usr/local/opt/node@14/bin:$PATH"
```

For Windows/Linux nvm user:
```shell
$ nvm install 14
$ nvm list
$ nvm use version-number
```

With the right Node version, run:
```shell
$ npm install
```

_Note: If you don't have npm installed this you can skip this final step as a "snyk test" will not work without a **package-lock.json** file or the "**node_modules**" folder_

* Once npm is installed run a Snyk CLI test as follows

```shell
❯ snyk test --all-projects

Testing /Users/jiajun/workspace/github/juice-shop...

Tested 898 dependencies for known issues, found 37 issues, 52 vulnerable paths.


Issues to fix by upgrading:

  Upgrade concurrently@5.3.0 to concurrently@6.0.0 to fix
  ✗ Regular Expression Denial of Service (ReDoS) [High Severity][https://snyk.io/vuln/SNYK-JS-ANSIREGEX-1583908] in ansi-regex@4.1.0
    introduced by concurrently@5.3.0 > yargs@13.3.2 > string-width@3.1.0 > strip-ansi@5.2.0 > ansi-regex@4.1.0 and 8 other path(s)

  Upgrade express-jwt@0.1.3 to express-jwt@6.0.0 to fix
  ✗ Regular Expression Denial of Service (ReDoS) [Low Severity][https://snyk.io/vuln/npm:moment:20170905] in moment@2.0.0
    introduced by express-jwt@0.1.3 > jsonwebtoken@0.1.0 > moment@2.0.0
    
...

  ✗ Use After Free [High Severity][https://snyk.io/vuln/SNYK-JS-NODESASS-541000] in node-sass@4.14.1
    introduced by node-sass@4.14.1
  No upgrade or patch available
  ✗ Out-of-bounds Read [Medium Severity][https://snyk.io/vuln/SNYK-JS-NODESASS-541002] in node-sass@4.14.1
    introduced by node-sass@4.14.1
  No upgrade or patch available


License issues:

  ✗ GPL-3.0 license (new) [High Severity][https://snyk.io/vuln/snyk:lic:npm:qrious:GPL-3.0] in qrious@4.0.2
    introduced by anuglar2-qrcode@2.0.9998 > qrious@4.0.2



Organization:      workshop
Package manager:   npm
Target file:       frontend/package.json
Project name:      frontend
Open source:       no
Project path:      /Users/jiajun/workspace/github/juice-shop
Licenses:          enabled

Tip: Run `snyk wizard` to address these issues.


Tested 2 projects, 2 contained vulnerable paths.

```
# CI/CD Steps

Snyk integrates with your CI/CD pipelines to provide the ability to prevent critical vulnerabilities from going into production. Adequate security gates are essential in ensuring the appropriate quality is delivered in an automated fashion and nothing serious slips through by accident. 

### Step 9 - Retrieve the Snyk API token from Snyk App

* Login to http://app.snyk.io
* Navigating to **Settings** -> **Service Accounts**
* Create a new service account, _**ghactions**_
* Assign the role, _**Org Admin**_

![service account](https://user-images.githubusercontent.com/25560159/194320725-88f152ca-7c61-4be4-bcaf-d10585fd88c0.png)

* Once created, copy the API token to clipboard.

### Step 10 - Add the Snyk API token into the GitHub repository secret

* Navigate to your forked juice-shop repository
* Navigate to **Settings**
* Click on **Secrets**

![secrets](https://user-images.githubusercontent.com/25560159/194323963-2981ce05-0d14-4927-bf58-8cdaabf796b5.png)

* Click on **Actions**
* Click on **New repository secret**

![secrets2](https://user-images.githubusercontent.com/25560159/194324503-cce8019a-c2c4-4493-8499-5dda853949f5.png)

* Use **SNYK_TOKEN** as the name of the secret
* Paste your Snyk API token from Step 10

![secrets3](https://user-images.githubusercontent.com/25560159/194324724-1ec23f42-3ea2-4119-99bf-7284f3c42e3c.png)

* Click **Add secret**

### Step 11 - Create the GitHub Actions workflow

* Navigate to your forked juice-shop repository
* Navigate to **Actions**
* Click on new workflow

![github_actions](https://user-images.githubusercontent.com/25560159/194322229-5466793b-262f-4847-90b4-500e8746116f.png)

* Click on _**Set up a workflow yourself**_

![github_actions2](https://user-images.githubusercontent.com/25560159/194322591-3d99c787-43bc-45ca-8f52-9bc0fcd985a8.png)

* Copy and paste the following to the main.yml:

```bash
name: "Snyk Code and Snyk Open Source Test"

on:
  push:
    branches:
    - master

jobs:
  Pipeline-Job:
    # Configure Environment
    name: 'Snyk Test'
    runs-on: ubuntu-latest
    env: 
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
       
    steps:
    # Checkout Code
    - name: Checkout Code
      uses: actions/checkout@v1

    # Install and Authenticate to Snyk
    - name: Install Snyk & Authenticate
      run: |
         sudo npm install -g snyk
         echo ${SNYK_TOKEN}
         snyk auth ${SNYK_TOKEN}
    # Run Snyk Code
    - name: Snyk Code test
      run: |
         snyk code test
      continue-on-error: true
    # Run Snyk Open Source
    - name: Snyk Open Source test
      run: |
         snyk test
      continue-on-error: true
```

* Click on **Start commit**
* Click on **Commit new file**

![actions3](https://user-images.githubusercontent.com/25560159/194326242-5b6b4eb2-2e68-418b-bbd1-7d886de1d44c.png)

Congratulations, you have completed. Thanks for attending and completing this workshop

![alt tag](https://i.ibb.co/7tnp1B6/snyk-logo.png)

<hr />
JJ [jj.ng at snyk.io] is a Solution Engineer at Snyk APJ 
<br/>




