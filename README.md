# Personal Life OS · Cloud Edition

Public program only. Never commit personal settings, backups, health records, tokens or private data here. Upload files in this folder to a public repository root; enable Pages from main / root. HTTPS is required for PWA install.

Personal data stays in browser storage or a dedicated private GitHub repository. Only grant a fine-grained token for that private repository, Contents read/write. Never publish the private repository or turn on Pages there. Git history may retain old records. No remote images or third-party JavaScript.

## V4.0.2: encrypted device authorization

Configure each device/browser separately with its own GitHub token and an independent unlock passphrase (at least 12 characters; prefer a long unique phrase). The token is encrypted with AES-256-GCM and a random 96-bit nonce. A non-exportable key is derived using PBKDF2-SHA-256 (600,000 iterations, random 128-bit salt). The repository name and vault version are authenticated with the ciphertext. Only the encrypted envelope and derivation parameters are stored in IndexedDB. Neither the passphrase nor the derived key is persisted. The token and passphrase are not part of life-data exports, reports, or GitHub synchronization.

Reload/reopen starts locked. Unlock once, then changes synchronize while the app is open, on returning to the foreground, and when connectivity returns. This does not provide reliable closed-app/background synchronization on iPhone. Manual locking clears the in-memory credential and aborts pending requests; a write already accepted by GitHub cannot be recalled. HTTP 401 locks the credential and asks for a replacement token. Clearing this browser's saved authorization does not delete life records or revoke the token at GitHub. Close other unlocked windows as well; revoke a lost device's token in GitHub settings.

This is a browser vault, not an OS keychain or biometric login. It protects stored tokens from plaintext exposure, subject to passphrase strength. It does not encrypt life records already stored in localStorage or protect against malicious same-origin scripts capturing an unlock passphrase/token. GitHub Pages projects under the same hostname share an origin. Use only trusted code on that origin; a dedicated origin/profile reduces exposure. Browser data clearing/eviction can remove the vault, requiring token setup again. If the passphrase is forgotten, clear the local authorization and configure a token again; life records remain intact.

Verification: real WebCrypto round trips and tamper/wrong-passphrase rejection; simulated IndexedDB transaction failure, fresh-context unlock, credential expiry, offline recovery, and lock during sync; 12 simulated view renders. Physical Safari/iPhone and Edge/PWA behavior still require device acceptance testing.

Existing V4 backups are importable; import replaces local state. Back up first. New fields can be entered in Settings > 私人配置.
