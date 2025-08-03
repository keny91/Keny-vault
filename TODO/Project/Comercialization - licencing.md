#licencing #comercialization

If you want to **sell an integrated piece of hardware that includes software**, you _must_ ensure all components—binaries, libraries, and code—comply with commercial redistribution rules. This involves licensing, export restrictions, and possibly even hardware-related patents.

Let’s break it down into what you can do **to check for non-redistributable components** and what you should **absolutely be aware of**:

---

### 🔍 How to Check for Non-Redistributable Libraries or Software

#### 1. **Check All Installed Packages and Their Licenses**

Depending on your OS (Linux most likely in embedded), get a list of installed packages and their licenses:

- **Debian/Ubuntu-based:**

```
dpkg-query -W -f='${Package} ${Version} ${License}\n' | less
```

(License info might not always be present—see next point.)
    
- Use `apt-cache`:

```
apt-cache show <package-name> | grep -i license
```

- RedHat/CentOS/Fedora:

```
rpm -qa --qf "%{NAME}-%{VERSION} %{LICENSE}\n"
```


#### 2. **Use `license-checker` or SPDX tools**

- If your project uses **Node.js**, run:

```
npx license-checker --summary
```

- For any language, tools like FOSSology, [scancode-toolkit](https://github.com/nexB/scancode-toolkit), or SPDX tools can scan your source code tree and list licenses, including incompatible ones.
    

#### 3. **Identify Binary Dependencies**

If you ship precompiled binaries (e.g., in C/C++), use tools to inspect shared libraries:

- **ldd**:
  
```
ldd your_binary
```

- Then trace each `.so` file and verify its origin and license.
    
- Use **`strace`** or **`lsof`** during runtime to catch runtime library or file access.
    

#### 4. **Source License Auditing**

If you include 3rd-party source code, check for:

- `LICENSE`, `COPYING`, or `NOTICE` files.
    
- License headers in individual source files.
    
- Any `dependencies.txt`, `requirements.txt`, or lock files (like `package-lock.json`) in language-specific projects.
    

---

### 🚩 Common Licenses That Are **NOT** Commercially Redistributable (or Restrictive)

|License|Issue|
|---|---|
|**GPLv3**|Requires you to open-source all derivative work and ship source code.|
|**AGPL**|Requires source release even for remote network use (e.g. a web server).|
|**Creative Commons NC (Non-Commercial)**|You **cannot** use it in commercial products.|
|**Proprietary**|Often forbids redistribution entirely or charges license fees.|
|**MPL/LGPL**|May allow dynamic linking, but not static linking without disclosure.|

Use tools like `scancode-toolkit` to tag problematic licenses automatically.

---

### ✅ Licenses That Are Generally OK for Commercial Use

|License|Notes|
|---|---|
|**MIT / BSD / Apache 2.0**|Very permissive. Attribution required.|
|**Zlib / Boost**|Also permissive.|
|**LGPL** (careful!)|OK if dynamically linked and unmodified. Static linking may be a problem.|

### ⚠️ Extra Things to Be Aware Of When Selling Hardware + Software

#### 1. **Export Control Regulations**

- Encryption-related software may be restricted under **EAR (U.S.)** or **dual-use** regulations in the EU.
    
- Check if your software includes OpenSSL, SSH, VPNs, etc.
    

#### 2. **Patents**

- Some codecs (e.g., MP3, H.264) require royalty payments if used commercially—even if the software is open-source.
    
- Avoid codecs or crypto libraries without verifying their **patent status**.
    

#### 3. **Trademark Use**

- Using logos, names (e.g., “Raspberry Pi”), or branding from third parties may violate trademark laws.
    

#### 4. **Hardware Drivers / Blobs**

- Some GPU or WiFi drivers are binary-only and not licensed for redistribution.
    
- E.g., Broadcom WiFi firmware in Raspberry Pi has specific terms.
    

---

### ✅ Best Practices for Safety

- Run a **full license scan** on your source tree and binaries.
    
- Create a **Software Bill of Materials (SBOM)** (use SPDX or CycloneDX formats).
    
- Avoid GPL/AGPL unless you’re OK with open-sourcing your product.
    
- Prefer MIT/BSD/Apache 2.0 libraries.
    
- Read **redistribution clauses** in licenses.
    
- Document everything.
    

---

### 🛠 Recommended Tools

|Tool|Purpose|
|---|---|
|`scancode-toolkit`|Scan source code and packages for license issues|
|`license-checker`|Node.js license reports|
|`reuse` (FSFE)|Helps make license info clear in your project|
|FOSSology|Enterprise-level license compliance analyzer|
|`ldd`, `strace`, `lsof`|Trace binary dependencies|