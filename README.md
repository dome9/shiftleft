# CheckPoint **shiftleft**

## Background

The Check Point CloudGuard platform provides cloud native security, with advanced threat prevention for all assets and workloads – in public, private, hybrid or multi-cloud environment – providing unified security to automate security everywhere. As part of the CloudGuard family, Check Point **shiftleft** brings CloudGuards security abilities to detect and prevent risk in cloud deployments into the CI/CD pipeline. **shiftleft** provides a single interface for multiple CI/CD security steps, including scanning your Infrastructure-as-Code (IaC) templates for risk, checking your software for known vulnerabilities, and scanning container images for security issues.

## Prerequisites

You'll need a CloudGuard account to use **shiftleft.** If you're organization isn't already using Check Point's Cloud Guard, head over to [the Cloud Guard portal](https://secure.dome9.com/v2/register/invite) to create an account.

## Installation

To use **shiftleft** you will need to:

1. Install the shiftleft CLI binary
2. Generate an autorization token in the CloudGuard portal
3. Setup the token in your environment

### Detailed Instructions
Choose your desired platform:
<details>
    <summary>Windows</summary>

| Step | Description |
| ---- | ----------- |
| 1 | Download the [x64](https://shiftleft-prod.s3.amazonaws.com/blades/shiftleft/bin/windows/amd64/0.0.24/shiftleft.exe) or [386](https://shiftleft-prod.s3.amazonaws.com/blades/shiftleft/bin/windows/386/0.0.24/shiftleft.exe) shiftleft standalone binary. |
| 2 | Save the `shiftleft.exe` file in a directory in your current `PATH` |
| 3 | Generate a CloudGuard access token [in the CloudGuard portal](https://secure.dome9.com/v2/settings/credentials). <details><summary>*Show me how*</summary>![](https://secure.dome9.com/v2/assets/images/shiftleft/create-api-key.PNG)<br> ![](https://secure.dome9.com/v2/assets/images/shiftleft/new-api-key.PNG)</details> |
| 4 | Set the CloudGuard ID and secret in your environment. In a windows command terminal type:<code>setx CHKP_CLOUDGARD_ID the-token-id-from-step-3<br>setx CHKP\_CLOUDGUARD\_SECRET the-secret-from-step-3</code>
| 5 | Launch a new command terminal, and verify that **shiftleft** is properly installed: <pre><code>C:\\>shiftleft –-version
0.0.20 </code></pre>|

</details>

<details>
    <summary>Linux</summary>

| Step | Description |
| ---- | ----------- |
| 1 | Download the [x64](https://shiftleft-prod.s3.amazonaws.com/blades/shiftleft/bin/linux/amd64/0.0.24/shiftleft) or [386](https://shiftleft-prod.s3.amazonaws.com/blades/shiftleft/bin/linux/386/0.0.24/shiftleft) shiftleft standalone binary. |
| 2 | Make shiftleft executable and move the file into a directory in your current `PATH`, for example:<pre><code>chmod +x shiftleft<br>mv shiftleft ~/bin </code></pre>|
| 3 | Generate a CloudGuard access token [in the CloudGuard portal](https://secure.dome9.com/v2/settings/credentials). <details><summary>*Show me how*</summary>![](https://secure.dome9.com/v2/assets/images/shiftleft/create-api-key.PNG)<br> ![](https://secure.dome9.com/v2/assets/images/shiftleft/new-api-key.PNG)</details> |
| 4 | Set the CloudGuard ID and secret in your environment as appropriate. For example, add the following to `~/.profile`<pre><code>export CHKP_CLOUDGARD_ID=*the-token-id-from-step-3*<br>export CHKP_CLOUDGUARD_SECRET=*the-secret-from-step-3*</code></pre> |
| 5 | Launch a new command terminal, and verify that **shiftleft** is properly installed: <pre><code>$shiftleft –-version<br>0.0.20 </code></pre>|

</details>

<details>
    <summary>Mac OS</summary>

| Step | Description |
| ---- | ----------- |
| 1 | Download the [x64](https://shiftleft-prod.s3.amazonaws.com/blades/shiftleft/bin/darwin/amd64/0.0.24/shiftleft) shiftleft standalone binary. |
| 2 | Make shiftleft executable, allow it to run unsigned, and move the file into a directory in your current `PATH`, for example:<pre><code>chmod +x shiftleft<br>spctl --add shiftleft<br>sudo mv shiftleft /usr/bin </code></pre>|
| 3 | Generate a CloudGuard access token [in the CloudGuard portal](https://secure.dome9.com/v2/settings/credentials). <details><summary>*Show me how*</summary>![](https://secure.dome9.com/v2/assets/images/shiftleft/create-api-key.PNG)<br> ![](https://secure.dome9.com/v2/assets/images/shiftleft/new-api-key.PNG)</details> |
| 4 | Set the CloudGuard ID and secret in your environment as appropriate. For example, add the following to `~/.bash_profile`<pre><code>export CHKP_CLOUDGARD_ID=*the-token-id-from-step-3*<br>export CHKP_CLOUDGUARD_SECRET=*the-secret-from-step-3*</code></pre> |
| 5 | Launch a new command terminal, and verify that **shiftleft** is properly installed: <pre><code>user-mbp:~ user$ shiftleft –-version<br>0.0.20</code></pre> |

</details>

## Blades

**shiftleft** is a CLI tool framework that allows access to multiple services. The services are called blades, and each individual blade provides a specific service.

The blades currently available are:
| Blade Name | Description | Usage Example |
| ---------- | ----------- | ------------- |
| iac-assessment | Scans Infrastructure-as-code templates, enabling DevOps and security teams to identify insecure configurations | `shiftleft iac-assessment -h` |
| image-scan | Scans container images for security risks and vulnerabilities | `shiftleft image-scan -h` |
| sourceguard | source-code security and visibility into the risk analysis of projects | `shiftleft sourceguard -h` |

## Use Cases

There are many ways the shiftleft framework can be used, but to provide a basic sense of how the tool can be used, here are some sample use cases:

### Scanning Terraform Templates for Risk

|You have a Terraform configuration in the `my_config.tf` file, and you want to run ruleset number -64 on this file to check if it is compliant.|
|-|
```bash
shiftleft iac-assessment -p my_config.tf -r -64 
```

Please refer to the detailed documentation for the iac-assesment blade below.

### Scanning Container Images for Vulnerabilities 
| You have a container image called `my_container.tar` that you want to scan for vulnerabilities. |
|-|
```bash
shiftleft image-scan -i my_container.tar
```

## Updates

The **shiftleft** CLI tool will automatically check for updates to the tool and any blades that you use, each time it's run.

