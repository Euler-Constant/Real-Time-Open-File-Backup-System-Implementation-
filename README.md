# ROFBS Paper Implementation

> Personal Implementation of the techniques used in "Impact of File-Open Hook Points on Backup Ratio in ROFBS on XFS" (Higuchi et al., 2026)

## Paper

**Title**: Impact of File-Open Hook Points on Backup Ratio in ROFBS on XFS
**Authors**: Kosuke Higuchi, Ryotaro Kobayashi
**Link**: https://arxiv.org/abs/2603.16364

## Summary of the notes (in rofbs.md)
- **Paper summary**
- **System analysis** 
- **Personal conjecture**
- **Insights found**

## TL;DR:

ML-based ransomware detection has an unavoidable detection time gap, which occurs in the window between when ransomware starts encrypting and when the model actually catches and kills it. This gap has two components: response time (feature collection + classification) and kill time (actually terminating the process). Files encrypted during this window are lost to the threat.

ROFBS takes a more active approach to the problem. Using eBPF hooks at the kernel level, it monitors for file open events (xfs_file_open). The moment a file is accessed, it suspends the accessing process, Creates a .tmp copy of the file as a backup, and resumes the process, which is deliberate because ransomware typically skips those extensions to avoid breaking the OS.

## Implementation

Note: The experiment was performed in what was a hardened instance of Arch Linux. Some things may break if you test them in different environments (It might even break in the same environment, no less T_T)


Clone the repo: git clone https://github.com/Euler-Constant/Real-Time-Open-File-Backup-System-Implementation-.git

Primarily for learning purposes.
