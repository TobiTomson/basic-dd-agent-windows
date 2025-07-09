# Datadog Agent Configuration for Windows

This repository contains configuration files for the Datadog Agent on Windows.

## Features Enabled

By using these configuration files, the following Datadog Agent features will be enabled:

- **Process Monitoring**: Collects live process data from your Windows host.
- **Cloud Network Monitoring**: Monitors network traffic and performance for cloud environments.
- **Universal Service Monitoring**: Automatically detects and monitors service-to-service communication.
- **Network Path Monitoring**: Monitors network path performance to `app.datadoghq.com`.
- **Windows Event Log Collection**: Collects logs from the Application, System, Security, and PowerShell event channels on your Windows host. This enables visibility into system, application, and security events for troubleshooting and compliance.

## Usage

1. **Install the Datadog Agent**  
	Download and install the [Datadog Agent for Windows](https://docs.datadoghq.com/agent/basic_agent_usage/windows/) with all features installed locally (important, else the [network monitoring support](https://docs.datadoghq.com/network_monitoring/cloud_network_monitoring/setup/?tab=agentlinux#windows-os) will be missing).

2. **Copy Configuration Files**  
	Copy the contents of this repository to the `%ProgramData%\Datadog` directory on your Windows machine.

3. **Set Your API Key**  
	Open `conf.yaml` and replace the `API_KEY` placeholder with your actual Datadog API key.

	For instructions on obtaining and using API keys, see the [Datadog API Keys documentation](https://docs.datadoghq.com/account_management/api-app-keys/).

4. **Restart the Datadog Agent**  
	After making any changes to the configuration files, you must restart the Datadog Agent for the changes to take effect.  
	For more information and agent commands, see the [Datadog Agent command documentation](https://docs.datadoghq.com/agent/basic_agent_usage/windows/?tab=standardinstallation#agent-commands).

5. **Supported Windows Versions**  
	Ensure you are running a Windows version supported by the latest Datadog Agent. Some features may not work on unsupported versions.  
	See the list of supported Windows versions here: [Datadog Agent Supported Platforms](https://docs.datadoghq.com/agent/supported_platforms/?tab=windows)

## Configuration File Overview

- **datadog.yaml**
  - Sets the Datadog API key (`api_key`) used for authentication and data submission.
  - Sets the Datadog site (`site`) to `datadoghq.eu`, which determines the Datadog region your data is sent to.
  - You can change the API key to your own, and set the site to another Datadog region if needed.
  - For more configuration options, see the [Datadog Agent configuration documentation](https://docs.datadoghq.com/agent/guide/agent-configuration-files/) and review the commented-out sample parameters in this file.

- **system-probe.yaml**
  - Enables the Network Module (`network_config.enabled: true`), which collects network performance and flow data.
  - Enables Universal Service Monitoring (`service_monitoring_config.enabled: true`), which detects and monitors service-to-service communication automatically.
  - Enables the Traceroute Module (`traceroute.enabled: true`), which allows the agent to perform traceroute operations for network path analysis.
  - You can disable or further configure these modules by changing their respective `enabled` values or adjusting additional parameters in this file.
  - For more configuration options, see the [System Probe documentation](https://docs.datadoghq.com/network_monitoring/cloud_network_monitoring/setup/) and review the commented-out sample parameters in this file.

- **conf.d/network_path.d/conf.yaml**
  - Configures the Network Path integration to monitor the endpoint `app.datadoghq.com` on port 443 using the TCP protocol.
  - You can change the `hostname`, `port`, or `protocol` to monitor a different endpoint or use a different protocol.
  - For more configuration options, see the [Network Path documentation](https://docs.datadoghq.com/integrations/network_path/) and review the commented-out sample parameters in this file.

- **conf.d/ntp.d/conf.yaml**
  - No active (uncommented) configuration. The default NTP monitoring settings will be used, which typically means monitoring the default NTP server.
  - To monitor a specific NTP server or adjust thresholds, uncomment and edit the relevant sections.
  - For more configuration options, see the [NTP check documentation](https://docs.datadoghq.com/integrations/ntp/) and review the commented-out sample parameters in this file.

- **conf.d/win32_event_log.d/conf.yaml**
  - Enables collection of Windows Event Logs using the modern event log API with `legacy_mode: false` for improved performance and reliability.
  - By default, collects events from the `System` channel. You can add more channels or customize filters, queries, and advanced options as needed.
  - For more configuration options, see the [Windows Event Log documentation](https://docs.datadoghq.com/integrations/windows_event_log/) and review the commented-out sample parameters in this file.