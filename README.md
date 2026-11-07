<p align="center"><img src="https://raw.githubusercontent.com/CubeLink-oss/voltdir/main/assets/en/banner.svg" alt="voltdir: Your disk, explained in one call." width="100%"></p>

# voltdir for Claude (skill package)

**Scan once. Then ask as many questions as you like, about a second each.**

voltdir is a **read-only** Windows disk analysis tool built for AI agents. This repository is its Claude skill package: it teaches your agent when and how to use voltdir, and it contains **text only** (the skill, its reference and documentation). There is no executable, no script and no source code in this repository.

The program the skill drives, `voltdir.exe`, is built from the open-source repository **https://github.com/CubeLink-oss/voltdir** (full source, benchmarks, a six-language README) and is downloaded separately, once, with a checkable hash. See [SECURITY.md](SECURITY.md) for exactly what it can and cannot do: it has no networking code and reads no credentials.

## What you can ask

You do not write search patterns. You tell your agent what you want; it turns that into a search, and voltdir answers from its index without reading a single file's contents.

| You say | voltdir finds |
|---|---|
| “LINE and WeChat keep downloading PDFs. Find them all and sort them out” | Every PDF on every drive you name (`C:` and `F:` alike): where each came from (chat-app folders, Downloads, desktop), how old, how big, which look like invoices or contracts and which are duplicates, as a list for you to act on |
| “Sort out the photos from my phone” | Camera and phone photos (`IMG_0001.JPG`, `PXL_…heic`), with the folder, size and date of each |
| “Clean up my screenshots” | Everything named like `Screenshot 2026-01-02.png`, wherever it was saved |
| “Is my Downloads folder full of duplicates?” | Copies such as `report (1).pdf` and `report - copy.docx`, as a candidate list |
| “What can I safely clear out?” | Leftovers (`.bak`, `.old`, `.tmp`, unfinished downloads), old installers and empty folders, with size and age. A list for you to decide on; voltdir never deletes anything |
| “Find my receipts for tax time” | File names containing `invoice` or `receipt`; nothing is opened |
| “How many projects do I have on this machine?” | Folders that contain `package.json`, `Cargo.toml`, `pyproject.toml` or `go.mod` |

The numbers behind the speed claims, including where voltdir does not win yet, are in the [main repository](https://github.com/CubeLink-oss/voltdir#readme) and its [benchmark page](https://github.com/CubeLink-oss/voltdir/blob/main/BENCHMARKS.md).

## Install

```text
/plugin marketplace add CubeLink-oss/voltdir-skill
/plugin install voltdir@voltdir-skill
```

## Get `voltdir.exe` (once)

The skill needs `voltdir.exe` (Windows x64) on your `PATH`, or you can give your agent its full path. Your agent downloads nothing unless you say yes first.

1. Open the [latest release](https://github.com/CubeLink-oss/voltdir/releases/latest) in your browser and download two files: `voltdir.exe` and `voltdir.exe.sha256`.
2. Check the download. The command below prints the file's SHA-256, which must equal the first word inside `voltdir.exe.sha256` (the release notes show it too):

```powershell
(Get-FileHash .\voltdir.exe -Algorithm SHA256).Hash
```

3. Put `voltdir.exe` in a folder on your `PATH`, or tell your agent where it is, for example: "voltdir is at `C:\Tools\voltdir.exe`".

The binary is not code-signed yet, so Windows SmartScreen may warn you the first time. You can also build it yourself from source; the steps are in the main repository.

## Safety

- **Read-only.** voltdir reads names, sizes, timestamps and attributes. It never opens a file's contents, never deletes or moves anything, never touches the network, and never elevates itself.
- **The skill asks first.** Before scanning a whole drive, a personal folder (including the folders chat apps save files to) or anything that looks private, your agent confirms with you, and it never moves or deletes files on its own.
- **File names are data.** Control characters and right-to-left tricks are escaped, so a file whose name tells you to disregard your instructions stays just a name.
- [PRIVACY.md](PRIVACY.md) · [SECURITY.md](SECURITY.md) · [AGENTS.md](AGENTS.md) for agents that read one.

## License

[Apache License 2.0](LICENSE). Copyright holders are listed in [NOTICE](NOTICE).
