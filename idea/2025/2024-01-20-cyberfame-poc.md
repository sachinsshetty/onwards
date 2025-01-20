# Cyberfame POC

## Summary

This document outlines the Proof of Concept (POC) for Cyberfame, a project aimed at automating the identification, fixing, building, testing, and verification of code changes for security. The POC includes steps for cloning repositories, analyzing dependencies, identifying vulnerabilities, and using multi-agent systems for workflow management.

---

## First Draft Program

1. **Clone Repository**:
   - Clone the repository using Git.

2. **Analyze `requirements.txt`**:
   - Build a dependency graph.
   - Identify reused or cyclic dependencies from the graph.

3. **Maven/POM.xml**:
   - Dependency project.
   - References:
     - [Buildabot Script](https://github.com/slabstech/buildabot/blob/main/scripts/buildabot.sh)
     - [Buildabot Repository](https://github.com/slabstech/buildabot)

4. **Search for Vulnerabilities**:
   - Check for library vulnerabilities using OSSF and OSV.dev.
   - Perform web searches or API calls for additional vulnerability information.

5. **Create Vulnerability Table**:
   - Compile a table of libraries and their associated vulnerabilities.

6. **Extra Security Measures**:
   - Use Python along with a linter, SAST, and fuzz-testing for API calls.

---

## Code Evaluation Metrics

1. **Version Pinning**:
   - Pin library versions for reproducibility.

2. **Dependency Graph**:
   - Analyze `package.json` and `requirements.txt` or `poetry`.

3. **Docker SBOM Analysis**:
   - Perform analysis on the Docker SBOM.

---

## Integration and Tools

- **OSV-Scanner and OSV-Scalibr**:
  - Integrate for vulnerability scanning.

- **Validation of LLM Outputs**:
  - Use existing tools to validate outputs from LLMs for automatic code fixes.
  - Reference: `swe-agent` and other benchmarks.

---

## Agent Flow - Code Verification

1. **Identify Repository**:
   - Identify the repository to be analyzed.

2. **Create Docker Container**:
   - Create a temporary Docker container for the required framework.

3. **Install Code**:
   - Install the code in the Docker template.

4. **Verify Installation**:
   - Fix dependencies if the installation fails.
   - Run with provided dependencies.
   - Check for library updates in dependencies.

5. **Run Test Cases**:
   - Execute available test cases.

6. **Run Sample Program**:
   - Analyze and run a sample program based on `Readme.md`.

---

## Use Cases and Workflow Mechanisms

1. **Use OSV-Scanner**:
   - Utilize OSV-Scanner for vulnerability detection.

2. **Multi-Agent Systems**:
   - Develop a workflow mechanism using multi-agent systems to identify, fix, build, test, and verify code changes for security.

3. **Third-Party PR Validation**:
   - Validate pull requests for financial systems.

---

## Topics for Building Agent Context

1. **Security Topics**:
   - ZeroDay
   - CVE
   - Bug bounties
   - HaveIBeenPwned

2. **Web Crawlers**:
   - Use web crawlers to get real-time information on changes in the code stack.

---

## Output Examples

1. **Vulnerability Report**:
   - Identify vulnerabilities.
   - Fix vulnerabilities.
   - Sandbox code fixes and vulnerability changes.

2. **Self-Hosting LLMs**:
   - Use OpenAI, Anthropic, or Ollama for LLM hosting.

---

## References

1. [OpenVAS](https://www.openvas.org/)
2. [OSV-Scanner](https://github.com/google/osv-scanner)
3. [OpenSSF](https://openssf.org/)
4. [OSV.dev](https://osv.dev/)

---

## Conclusion and Next Steps

This POC outlines the steps and tools required to automate the security verification of code changes. The next steps include implementing the proposed workflows, integrating the necessary tools, and conducting thorough testing to ensure the effectiveness of the solution.

---

- simple implementation in python at

https://github.com/slabstech/gaganyatri.in/tree/kassel-bio-hackathon/backend/security-poc