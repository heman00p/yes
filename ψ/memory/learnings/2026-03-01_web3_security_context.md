# Web3 Wallet Security Context Requirements

Web3 providers like MetaMask strictly enforce a secure context for interaction. Developers must be aware that trying to access `window.ethereum` from a local file will likely fail due to security policies.

### Core Constraints:
1. **Forbidden File Protocol:** Accessing your application via `file:///C:/...` will prevent MetaMask from injecting its provider.
2. **Mandatory Origin:** You must serve your application from a recognized origin like `localhost` or `127.0.0.1` during development.
3. **Simple Workarounds:**
   - Use VS Code **Live Server** extension.
   - Run a quick Python server: `python -m http.server 8000`.
   - Use Node.js: `npx serve .`.

Failing to provide a proper server environment is the #1 cause of "Wallet not detected" errors for beginner Web3 developers.