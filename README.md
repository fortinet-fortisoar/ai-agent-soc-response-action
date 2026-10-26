# Release Information

- **Version**: 1.0.0

- **Certified**: Yes

- **Publisher**: Fortinet

- **Scope**: Containment and Remediation

- **Verified with Models**: Fortinet FortiAI (AI model Medium)

# SOC Response Action

Executes response and remediation actions, such as blocking or unblocking an IOC (IP Address, Domain, URL, File Hash (MD5/SHA1/SHA256), Host, Email Address), when the user requests it and sufficient context is available to act safely.

## Installation

This agent installs along with the FortiAI solution pack.

## Configuration

The SOC Response Framework agent ships with a configuration that has access to all shipped MCP servers. For custom configuration, refer to the *Configuration* section of the [FortiAI](https://github.com/fortinet-fortisoar/solution-pack-fortinet-advisor) solution pack documentation.

> [!Note]
> Refer to [Configuring MCP Servers](https://docs.fortinet.com/document/fortisoar/8.0.0/administration-guide/823139/mcp-servers#Configure_MCP_Servers) on FortiSOAR platform documentation for information on configuring a custom MCP server.

### Prerequisites

The following prerequisites must be met before using this agent:

- The FortiAI solution pack must be installed and configured with the Fortinet FortiAI connector.

  - To configure the FortiAI solution pack, refer to the [FortiAI](https://github.com/fortinet-fortisoar/solution-pack-fortinet-advisor/) solution pack documentation.
  - To configure the Fortinet FortiAI connector, refer to the [Fortinet FortiAI](https://docs.fortinet.com/fortisoar/connectors/fortinet-fortiai) connector documentation.

> [!Note]
> The FortiAI solution pack and the Fortinet FortiAI connector are preconfigured out-of-the-box with FortiSOAR `v8.0.1` and later.

## Input Parameters

The input must be provided as a JSON object.

| Parameter | Description                                                                                                                                                                                                                  |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `task`    | The natural language task for this agent to execute (e.g., block IOC, unblock IOC, create ticket, update ticket).                                                                                                            |
| `iocs`    | List of IOC objects to block or unblock. Each object must contain `value` and `type`. Required when the task is block/unblock. Can also be passed as a JSON string. Example: `[{"value": "8.8.8.8", "type": "IP Address"}]`. |
| `data`    | Free-form data used to create or update a ticket. Required when the task is create/update ticket. At least one of `iocs` or `data` must be provided.                                                                         |

## Response

The output is returned as a JSON object.

| Parameter     | Description                                                                                                                                     |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `answer`      | Human-readable description of what was done, the current state per IOC (completed, in progress, failed, unknown) and the overall task progress. |
| `confidence`  | Confidence percentage (e.g., "85%").                                                                                                            |
| `evidence`    | Per-target citation listing each IOC, its state, and supporting tool fields (status, IDs, record links, verbatim errors).                       |
