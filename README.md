
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="Content-Security-Policy" content="default-src 'self' https: 'unsafe-inline' 'unsafe-eval';">
    <title>KOROKOY - Next-Gen Cross-Chain Presale</title>
    <!-- Modern CSS Framework -->
    <link href="https://unpkg.com/modern-css-reset/dist/reset.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- WalletConnect Integration -->
    <script src="https://cdn.jsdelivr.net/npm/@walletconnect/web3-provider@1.7.8/dist/umd/index.min.js"></script>
    <script src="https://cdn.ethers.io/lib/ethers-5.7.umd.min.js" type="application/javascript"></script>
</head>
<body>
    <div id="app">
        <header class="app-header">
            <div class="branding">
                <img src="/korokoy-logo.svg" alt="KOROKOY Protocol" class="logo">
                <h1>KOROKOY Cross-Chain Presale</h1>
            </div>
            <div id="walletStatus" class="wallet-status">
                <button class="connect-button" id="connectButton">
                    <span class="loader" id="walletLoader"></span>
                    <span id="walletText">Connect Wallet</span>
                </button>
            </div>
        </header>

        <main class="presale-container">
            <div class="presale-card glassmorphic">
                <div class="chain-selector" id="chainSelector">
                    <button data-chain="1" class="chain-option eth">Ethereum</button>
                    <button data-chain="56" class="chain-option bsc">BNB Chain</button>
                    <button data-chain="137" class="chain-option matic">Polygon</button>
                </div>

                <div class="presale-stats">
                    <div class="time-progress">
                        <h3>Phase 1: Foundation Round</h3>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 65%"></div>
                        </div>
                        <div class="time-remaining" id="timeRemaining">
                            <countdown-timer end="2024-04-15T23:59:59"></countdown-timer>
                        </div>
                    </div>

                    <!-- Rest of the content remains similar with updated token details -->
                
                <div class="security-badges">
                    <div class="audit-badge">
                        <img src="/audited-by-hacken.svg" alt="Security Audited by Hacken">
                    </div>
                    <div class="liquidity-lock">
                        🔒 Liquidity locked via Team Finance
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- Script and style sections updated for new branding -->
    <style>
        :root {
            --primary: #4F46E5;
            --background: #0f172a;
            --accent: #10B981;
        }

        .chain-option {
            background: rgba(79, 70, 229, 0.1);
            color: var(--primary);
        }
    </style>
</body>
</html>
