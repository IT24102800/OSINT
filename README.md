# The Ghost Who Walked - CTF Challenge

## Overview

**Difficulty:** Hard  
**Theme:** Corporate Espionage & Whistleblower Investigation  
**Domains:** OSINT, Digital Forensics, Git Forensics, Steganography  

This CTF challenge simulates a real-world corporate investigation where participants must track down a whistleblower known as "NoOne" who leaked evidence of a massive data breach at the multinational conglomerate, Tech Vanguard.

## Challenge Summary

Participants start with a single image file and must use multiple OSINT techniques, metadata analysis, social media reconnaissance, and Git forensics to uncover the hidden flag.

### Scenario
Tech Vanguard has been rocked by a massive data breach. A whistleblower known only as "NoOne" has leaked internal documents proving the company illegally sold user data and manipulated financial records. The corporate security team tried to scrub all traces but wasn't thorough enough.

**Your mission:** Track down "NoOne" and obtain the full evidence stash they claim to have hidden online.

### Starting Point
- **File:** `DealIsDone.jpg`
- **Source:** Released by NoOne on an underground forum

## Learning Objectives

1. Apply advanced OSINT techniques (reverse image search, metadata analysis, social media enumeration)
2. Analyze file metadata using tools like `exiftool`
3. Correlate data from multiple sources to build a target profile
4. Conduct Git forensics to recover deleted files from commit history
5. Use critical thinking to follow a logical but non-obvious investigative trail
6. Document findings in a structured, professional manner

## Required Tools

| Tool | Purpose |
|------|---------|
| `exiftool` | Extract image metadata |
| Base64 Decoder | Decode encoded strings |
| Git | Clone repository, view history |
| GitHub Web UI | Browse commit history |
| OSINT Tools | Search for online profiles |
| Web Browser | Navigate to Pastebin, GitHub |

## Solution Path

### Phase 1: Image Analysis
1. Perform reverse image search on `DealIsDone.jpg`
   - *Result:* Generic stock photo, no direct leads
2. Run `exiftool DealIsDone.jpg`
   - *Finding:* Base64 string in XPComment/ImageDescription
   - `aHR0cHM6Ly9wYXN0ZWJpbi5jb20vNDZxeVBZekw=`
3. Decode Base64 using CyberChef
   - *Result:* `https://pastebin.com/46qyPYzL`

### Phase 2: Pastebin Investigation
1. Visit `https://pastebin.com/46qyPYzL`
   - *Findings:*
     - System backup log from Tech Vanguard
     - Email: `hal_jordan@protonmail.com`
     - Legacy token: `dGVjaHZhbmdhcmQtdXNlcg==`
     - Reference to: Tech Vanguard Forums (2019)

2. Decode the legacy token
   - `aHR0cHM6Ly9pdDI0MTAyODAwLmdpdGh1Yi5pby9PU0lOVC90ZWNodmFuZ3VhcmQtZm9ydW0vbWVtYmVyL3Byb2ZpbGUuaHRtbA==`
   - *Result:* `TechVanguard-member-haljordan`

### Phase 3: Forum Archive Investigation
1. OSINT search reveals archived forum profile
   - *URL:* TechVanguard-member-haljordan
2. Profile signature contains GitHub link
   - *Result:* NoOne's developer profile identified

### Phase 4: GitHub Investigation
1. Visit GitHub profile
   - *URL:* `https://TechVanguard/Hal Jordan`
2. Examine the repository
   - No obvious flag or secrets visible
3. Check commit history
   - Locate `secrets.txt` file in commit history
   - File was committed and then deleted

### Phase 5: Flag Submission
```
IE3132{gh0st_1n_th3_m4ch1n3}
```

## Hints

<details>
<summary><b>Hint 1</b></summary>
"The first clue is hidden in the image's metadata. Use exiftool to examine the file thoroughly."
</details>

<details>
<summary><b>Hint 2</b></summary>
"The Base64 string in the metadata points to a pastebin. Look for system logs and legacy references."
</details>

<details>
<summary><b>Hint 3</b></summary>
"TechVanguard was a forum from 2019. Search for archived profiles. The signature contains a URL link."
</details>

<details>
<summary><b>Hint 4</b></summary>
"Check the Git commit history. The flag was committed and then deleted. Look for secrets.txt."
</details>

## Red Herrings

| Red Herring | Why It's a Trap |
|-------------|-----------------|
| JWT Token | Decoy cryptographic token leading to JWT.io demo payload |
| admin/T3chP@ss2024! | Fake credentials |
| 192.168.1.105 | Internal IP address (not accessible externally) |
| 203.0.113.42 | TEST-NET IP range (can't be traced) |
| SHA256 Hashes | Filler content (trying to crack is wasted effort) |

## Stage Specification

| Field | Information |
|-------|-------------|
| Stage ID | CTF-OSINT |
| Title | The Ghost Who Walked |
| Domain | OSINT / Reconnaissance, Digital Forensics, Git Forensics |
| Difficulty | Hard |
| Flag | `IE3132{gh0st_1n_th3_m4ch1n3}` |
| Environment | Internet with hosted services |

## Author Notes

This challenge is designed to simulate a realistic corporate investigation scenario. Participants are expected to:

- Document their findings professionally
- Think critically about each clue
- Pivot between different data sources
- Use both technical tools and OSINT techniques

The trail is intentionally non-obvious and requires patience and attention to detail to complete successfully.

---

*Happy investigating, and remember: sometimes the ghosts are the ones walking among us.*
