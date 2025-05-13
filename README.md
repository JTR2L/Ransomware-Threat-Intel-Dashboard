# Ransomware Threat Intelligence Dashboard

## Overview
This repository contains a threat intelligence dashboard that leverages an ontology to analyze ransomware campaigns targeting Microsoft ecosystems (e.g., Exchange Server, Entra ID). Built with Azure Sentinel, Cosmos DB, Microsoft Graph Security API, and PowerShell, it demonstrates advanced threat analysis, automation, and compliance for a Microsoft Security Researcher role.

**Author**: Jason Trupp, cybersecurity professional with 25+ years securing Fortune 500 systems (Microsoft, Cisco, Bank of America). Expert in Microsoft Defender 365, Entra ID, zero-trust architecture, and PowerShell automation. Email: jason@recalledtolife.us.

## Project Objectives
- Design an ontology to map ransomware threats, vulnerabilities (CVEs), assets, and controls.
- Automate data ingestion and refreshes using PowerShell and Logic Apps.
- Visualize threat intelligence in Azure Sentinel with KQL-driven workbooks.
- Share insights via STIX 2.1 for interoperability with external partners.
- Ensure HIPAA-compliant data handling with Entra ID and Key Vault.

## Repository Structure
```
Ransomware-Threat-Intel-Dashboard/
├── scripts/
│   ├── Update-Ontology.ps1           # Automates CVE ingestion to Cosmos DB
│   ├── Additional_KQL_Queries.txt    # KQL queries for Sentinel Workbook
├── workbooks/
│   ├── Ransomware_Ontology_Workbook.json  # Sentinel Workbook for visualization
├── workflows/
│   ├── Ontology_Data_Refresh_Workflow.json  # Logic Apps for hourly data sync
├── stix/
│   ├── Ransomware_STIX_Bundle.json    # STIX 2.1 bundle for threat sharing
├── docs/
│   ├── Portfolio_Project_Outline.txt  # Project overview and timeline
├── README.md
```

## Key Components
1. **Ontology**:
   - Designed in Protégé (OWL/RDF), stored in Azure Cosmos DB (Gremlin API).
   - Classes: Threat (Ransomware), Vulnerability (CVE), Asset (Exchange Server, Entra ID), Control (Defender Policy).
   - Relationships: exploits, affects, mitigates, mappedTo (MITRE ATT&CK, NIST).
   - Example: `Threat:LockBit exploits Vulnerability:CVE-2025-1234 affects Asset:ExchangeServer`.

2. **Data Ingestion**:
   - **PowerShell Script** (`scripts/Update-Ontology.ps1`): Pulls MSRC CVE data and updates ontology in Cosmos DB.
   - **Microsoft Graph Security API**: Ingests Defender 365 alerts and Entra ID risky user data.
   - **Logic Apps Workflow** (`workflows/Ontology_Data_Refresh_Workflow.json`): Syncs updated triples to Sentinel’s `OntologyTriples` log hourly.

3. **Sentinel Workbook** (`workbooks/Ransomware_Ontology_Workbook.json`):
   - Tabs: Threat Analysis (Sankey diagram, TTP bar chart), Asset Exposure (pie chart, graph), Mitigation Controls (NIST mappings), Query Explorer.
   - KQL Queries (`scripts/Additional_KQL_Queries.txt`): Risk scoring, Entra ID risky users, threat timelines, NIST control mappings.

4. **STIX Export** (`stix/Ransomware_STIX_Bundle.json`):
   - Represents LockBit campaign (indicator, CVE, ATT&CK T1486, Defender control) in STIX 2.1.
   - Supports TAXII sharing with external partners.

## Setup Instructions
1. **Prerequisites**:
   - Azure subscription with Cosmos DB (Gremlin API), Sentinel, and Logic Apps.
   - Entra ID credentials with permissions for API connections.
   - PowerShell for local scripting.

2. **Ontology Setup**:
   - Model ontology in Protégé with sample triples (10 CVEs, 5 assets, 3 TTPs).
   - Deploy to Cosmos DB using `scripts/Update-Ontology.ps1`.

3. **Sentinel Configuration**:
   - Enable Defender 365 and Entra ID connectors in Sentinel.
   - Import `workbooks/Ransomware_Ontology_Workbook.json` into Sentinel Workbooks.
   - Run KQL queries from `scripts/Additional_KQL_Queries.txt`.

4. **Logic Apps Deployment**:
   - Deploy `workflows/Ontology_Data_Refresh_Workflow.json` per the deployment guide (docs/Logic_Apps_Deployment_Guide.txt).
   - Configure Cosmos DB and Sentinel connections with Entra ID managed identities.
   - Schedule hourly runs.

5. **STIX Sharing**:
   - Validate `stix/Ransomware_STIX_Bundle.json` with OpenCTI.
   - Share via TAXII server (e.g., OpenCTI instance).

## Usage
- **Threat Analysis**: Use the Sentinel Workbook to visualize ransomware threats (e.g., LockBit) mapped to CVEs and MITRE ATT&CK TTPs.
- **Asset Prioritization**: Identify high-risk assets (e.g., Exchange Server) with KQL risk scoring.
- **Compliance**: Map controls to NIST SP 800-53 for HIPAA compliance.
- **Automation**: PowerShell and Logic Apps ensure real-time ontology updates.
- **Interoperability**: Export STIX bundles for external collaboration.

## Demo
- **Video**: [Link to demo video, to be recorded] showcasing workbook visualizations and workflow execution.
- **Screenshots**: [To be added in `docs/screenshots/`] of Sankey diagrams, pie charts, and graph visualizations.

## Future Enhancements
- Add real-time Graph API webhooks for Defender alerts.
- Expand ontology with AI-based threat patterns.
- Integrate additional KQL queries for incident correlation.

## Contact
For feedback or collaboration, contact Jason Trupp at jason@recalledtolife.us or via LinkedIn.

## License
MIT License. See LICENSE file (to be added).