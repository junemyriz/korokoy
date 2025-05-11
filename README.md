# korokoy
meme presale its for non profit organization 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="Content-Security-Policy" content="default-src 'self' https: 'unsafe-inline' 'unsafe-eval';">
    <title>ZKSwap Presale 2.0</title>
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
                <img src="/logo.svg" alt="ZKSwap" class="logo">
                <h1>ZKSwap Presale 2.0</h1>
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
                        <h3>Stage 1: Early Access</h3>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 65%"></div>
                        </div>
                        <div class="time-remaining" id="timeRemaining">
                            <countdown-timer end="2024-03-31T23:59:59"></countdown-timer>
                        </div>
                    </div>

                    <div class="contribution-widget">
                        <token-input 
                            default-currency="USDC"
                            :supported-currencies="['ETH', 'USDT', 'USDC', 'DAI']"
                            :chain="selectedChain"
                            @amount-changed="updateContribution"
                        ></token-input>
                        
                        <button class="contribute-button" id="contributeButton" disabled>
                            Participate in Presale
                        </button>
                        
                        <div class="terms-agreement">
                            <input type="checkbox" id="kycCheck">
                            <label for="kycCheck">I confirm I'm not a restricted entity</label>
                        </div>
                    </div>
                </div>

                <div class="security-badges">
                    <div class="audit-badge">
                        <img src="/audited-by.svg" alt="Audited by CertiK">
                    </div>
                    <div class="liquidity-lock">
                        🔒 Liquidity locked for 2 years
                    </div>
                </div>
            </div>
        </main>
    </div>

    <script type="module">
        // Modern ES6 Implementation
        import { initWallet } from './wallet.js';
        import { presaleContract } from './contract.js';
        import { ChainManager } from './chain.js';
        
        class PresaleApp {
            constructor() {
                this.selectedChain = 1;
                this.userAddress = null;
                this.contributionAmount = 0;
                
                this.init();
            }

            async init() {
                this.chainManager = new ChainManager();
                this.wallet = await initWallet();
                this.registerEvents();
                this.updateUI();
            }

            registerEvents() {
                document.getElementById('connectButton').addEventListener('click', () => this.handleWallet());
                document.getElementById('contributeButton').addEventListener('click', () => this.handleContribution());
                document.querySelectorAll('.chain-option').forEach(btn => {
                    btn.addEventListener('click', () => this.switchChain(btn.dataset.chain));
                });
            }

            async handleWallet() {
                try {
                    await this.wallet.connect();
                    this.userAddress = this.wallet.getAddress();
                    this.updateUI();
                } catch (error) {
                    this.showError(`Wallet connection failed: ${error.message}`);
                }
            }

            async handleContribution() {
                if (!this.validateContribution()) return;
                
                try {
                    const tx = await presaleContract.contribute(
                        this.contributionAmount,
                        this.selectedChain
                    );
                    await tx.wait();
                    this.showSuccess('Contribution successful!');
                } catch (error) {
                    this.showError(`Transaction failed: ${error.message}`);
                }
            }

            validateContribution() {
                // Add validation logic
                return true;
            }

            updateUI() {
                // Update UI based on state
            }
        }

        // Initialize app
        window.addEventListener('load', () => new PresaleApp());
    </script>

    <style>
        /* Modern CSS Features */
        :root {
            --primary: #6366f1;
            --background: #0f172a;
            --glass: rgba(255, 255, 255, 0.05);
        }

        body {
            background: var(--background);
            font-family: 'Space Grotesk', sans-serif;
            color: white;
        }

        .glassmorphic {
            background: var(--glass);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 24px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }

        .presale-card {
            padding: 2rem;
            max-width: 800px;
            margin: 2rem auto;
        }

        .chain-selector {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .chain-option {
            padding: 0.75rem 1.5rem;
            border-radius: 12px;
            border: 1px solid transparent;
            background: rgba(99, 102, 241, 0.1);
            color: var(--primary);
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .chain-option.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
        }

        .contribution-widget {
            margin: 2rem 0;
        }

        .terms-agreement {
            margin-top: 1rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.9rem;
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            .presale-card {
                padding: 1rem;
                margin: 1rem;
            }
            
            .chain-selector {
                flex-direction: column;
            }
        }
    </style>
</body>
</html>
