# kql_playground
Description: "Interactive KQL training environment for threat hunters"
# 🔍 KQL Sandbox - Interactive Training Environment

Practice Kusto Query Language (KQL) for threat hunting and security analysis without needing Azure Sentinel, Microsoft Defender, or any cloud access.

**🌐 [Live Demo](https://scooter825.github.io/kql-sandbox/)** ← Replace with your actual GitHub Pages URL

## 📋 Overview

KQL Sandbox is a browser-based training tool for security analysts learning threat hunting with Kusto Query Language. It includes realistic security event data with hidden malicious activity for practicing detection techniques.

## ✨ Features

- 🔍 **Live KQL Query Execution** - Run queries instantly in your browser
- 📊 **Realistic Security Data** - 500+ DeviceProcessEvents, 300+ NetworkEvents, 200+ FileEvents
- 🚨 **Real Attack Techniques** - AMSI bypass, base64 obfuscation, lateral movement, mimikatz, certutil abuse
- 🏆 **Easter Egg Challenge** - Hidden message for learners to discover
- 💻 **100% Client-Side** - No backend, no setup, no API keys needed
- 🎨 **Dark Theme UI** - Familiar interface for security analysts

## 🚀 Quick Start

### Option 1: Use the Live Demo
Visit the [live demo](https://yourusername.github.io/kql-sandbox/) (no installation needed)

### Option 2: Download and Run Locally
1. Download `kql-sandbox-easter-egg.html`
2. Open it in any modern browser
3. Start writing KQL queries!

## 📚 Example Queries

### Hunt for Encoded PowerShell
```kql
DeviceProcessEvents 
| where ProcessCommandLine contains "-enc"
| order by Timestamp desc
```

### Find AMSI Bypass Attempts
```kql
DeviceProcessEvents 
| where ProcessCommandLine contains "AmsiUtils" 
   or ProcessCommandLine contains "amsiInitFailed"
```

### Detect Lateral Movement
```kql
DeviceProcessEvents 
| where FileName in ("psexec.exe", "wmic.exe")
| project Timestamp, DeviceName, FileName, ProcessCommandLine, AccountName
```

### Suspicious Base64 Payloads
```kql
DeviceProcessEvents 
| where ProcessCommandLine has_any ("-enc", "-encoded")
| where AccountName !in ("admin", "jsmith", "mdoe", "sysadmin", "developer")
```

### Summarize Activity by Device
```kql
DeviceProcessEvents 
| summarize count() by DeviceName
| order by count desc
```

## 🎯 Easter Egg Challenge

Hidden somewhere in the data is a secret message. Can you find it?

**Hints:**
- Look for unusual account names
- Check for suspicious ProcessIds
- Base64 decoding skills required
- First to find it wins bragging rights! 🏆

## 🛠️ Supported KQL Operators

- ✅ `where` - Filter data
- ✅ `contains` - String matching
- ✅ `has_any` - Match multiple values
- ✅ `==` - Exact match
- ✅ `order by` - Sort results
- ✅ `summarize count() by` - Aggregate data
- ✅ `project` - Select specific columns
- ✅ `take` / `limit` - Limit results

## 🎓 Learning Resources

- [Microsoft KQL Documentation](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)
- [KQL Quick Reference](https://learn.microsoft.com/en-us/azure/data-explorer/kql-quick-reference)
- [Threat Hunting with KQL](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/bg-p/MicrosoftSentinelBlog)

## 🤝 Contributing

Found a bug? Want to add more malicious samples? Contributions welcome!

1. Fork this repository
2. Create a feature branch
3. Submit a pull request

**Ideas for contributions:**
- Additional attack techniques
- More KQL operators
- Query validation/hints
- Export results to CSV
- Syntax highlighting

## 📝 Use Cases

- **SOC Analyst Training** - Practice queries without production access
- **Interview Prep** - Test KQL skills before security interviews
- **Workshop/Bootcamp Tool** - Hands-on learning for students
- **Red Team Practice** - Learn what blue teamers look for
- **Self-Study** - Learn threat hunting techniques offline

## ⚠️ Disclaimer

This tool contains simulated malicious data for educational purposes only. All malicious samples are synthetic and pose no actual threat. Do not use real malware samples in this sandbox.

## 📄 License

MIT License - See [LICENSE](LICENSE) file for details

## 🙏 Acknowledgments

Built for the security community to make KQL learning accessible to everyone.

---

**⭐ Star this repo if you find it useful!**

**🐛 Report issues:** [GitHub Issues](https://github.com/yourusername/kql-sandbox/issues)

**💬 Questions?** Open a discussion or reach out!
