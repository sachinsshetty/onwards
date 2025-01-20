Cyberfame POC

- Agent Flow - Code verification
  - Identify Repo
  - Create temporary docker container for required framework
  - Install code in Docker template
  - Verify sucessful instalation
    - Fix dependency if failed
    - Run with provided dependencies
    - check for library- update in dependency
  - Run test case if available
  - Run sample program by reading/analysis Readme.md

-- 

- Code evaluation metrics
  - version pinning libraries for reproducability
  - docker SBOM analysis
  - package.json / dependency graph
  - requirement.txt / poetry

--


osv-scanner and osv-scalibr could be integrated in the project for vulnerability scanning.

A combination of existing tools for evals should be build for validation of outputs of llm's for the automatic code fixes.
swe-agent and other benchmarks could be used as reference.

-- 

- Use OS-scanner
- Multi-agent systems as workflow mechanism to identify, fix, build, test and verify code changes for Security.
- 3rd party - PR validation for finance systems

- Topics to build agents context - web crawlers to get real time info for changes in Code stack
  - ZeroDay
  - CVE
  - bugbounties
  - haveibeenpawned

- Provide output with example video
  - What vulnerabilty were
    - identified
    - fixed
    - sandbox
        - code fixes
        - vulnerabilty cahnge
  - Self hosting LLM
    - OpenAI / Anthropic
    - Ollama



- Refernce
  - https://www.openvas.org/
  - https://github.com/google/osv-scanner
  - https://openssf.org/
  - https://osv.dev/
