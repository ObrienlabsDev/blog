
- Security Health Analytics (SHA)—Finds and reports misconfigurations of resources (disabled logs, extra IAM permissions, publicly exposed services). This is what we have currently enabled in our project and what detected the 76 vulnerabilities in our project.
- Web Security Scanner (WSS)—Scans publicly available web applications exposed via external IP addresses and checks for OWASP top 10 vulnerabilities.
- Event Threat Detection (ETD)—Provides log-based threat analysis that continuously monitors Google Cloud and Google Workspace logs to scan for potential threats.
- Container Threat Detection (CTD)—Detects the most common container runtime attacks in a Container Optimized OS.
- Virtual Machine Threat Detection—Analyzes memory of VM instances on the level of a Hypervisor and can detect suspicious activities happening in VM memory. Examples are unexpected kernel modules or running crypto-mining software.
- Cloud Run Threat Detection-Available for Premium or Enterprise Use kernel-level instrumentation to identify potential compromise of Cloud Run resources, including suspicious binaries. If enabled, all workloads will use the second generation execution environment when redeployed. Test your workloads on second generation before enabling.
- Vulnerability Assessment-Available for Premium or Enterprise Scan your Google Cloud and Amazon Web Services resources for common vulnerabilities and exposures (CVE).
- Notebook Security Scanner-Available for Premium or Enterprise Scan your Colab Enterprise notebooks for package vulnerabilities in the integrated open-source Python packages.
