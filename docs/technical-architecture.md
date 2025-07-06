# 🛠️ Architecture Technique CYBA Universe

## 🏗️ Vue d'Ensemble Système

CYBA Universe combine une **plateforme éducative gaming moderne** avec une **infrastructure blockchain sécurisée** pour créer une expérience Web3 unique.

```yaml
🌌 CYBA UNIVERSE ARCHITECTURE:
├── 🎮 Frontend Gaming (Next.js + Web3)
├── 🚀 Backend API (FastAPI + PostgreSQL)  
├── ⛓️ Smart Contracts (Solidity + Polygon)
├── 🎭 NFT Storage (IPFS + Metadata)
├── 💎 Token Economy (ERC-20 + Staking)
└── 🔒 Security Layer (Multi-signature + Audits)
```

---

## 🎮 Frontend Gaming Architecture

### **Stack Technique**
```typescript
// Tech Stack Principal
├── Framework: Next.js 14 (Pages Router)
├── Language: TypeScript 5.0+
├── Styling: TailwindCSS + Gaming Components
├── Web3: wagmi + ethers.js + RainbowKit
├── State: Zustand + React Query
├── Charts: Chart.js + D3.js
└── Testing: Jest + React Testing Library
```

### **Composants Gaming Clés**

#### **AvatarSelector Component**
```typescript
interface AvatarSelectorProps {
  onSelect: (avatarId: string) => void;
  userLevel: number;
  selectedAvatarId?: string;
  mode: 'registration' | 'switch' | 'preview';
}

export const AvatarSelector: React.FC<AvatarSelectorProps> = ({
  onSelect,
  userLevel,
  selectedAvatarId,
  mode = 'registration'
}) => {
  // Logique sélection avatar avec unlock conditions
  // Animation gaming et preview stats
  // Intégration Web3 pour NFT ownership
};
```

#### **Web3 Integration Layer**
```typescript
// hooks/useWeb3Gaming.ts
export const useWeb3Gaming = () => {
  const { address, isConnected } = useAccount();
  const { connect } = useConnect();
  
  const mintAvatar = async (avatarType: AvatarType) => {
    const contract = useContract({
      address: AVATAR_CONTRACT_ADDRESS,
      abi: AvatarABI,
    });
    
    return await contract.safeMint(address, {
      avatarType,
      baseStats: getAvatarBaseStats(avatarType),
      isGenesis: true
    });
  };
  
  const purchaseEquipment = async (equipmentId: string) => {
    // Interaction marketplace smart contract
  };
  
  return { mintAvatar, purchaseEquipment };
};
```

### **Gaming UI Components**

#### **Glass Morphism Gaming Style**
```css
/* styles/gaming.css */
.glass-card {
  @apply backdrop-blur-sm bg-gray-900/50 border border-cyan-500/30;
  @apply rounded-xl shadow-lg shadow-cyan-500/20;
}

.cyber-gradient {
  @apply bg-gradient-to-r from-cyan-400 via-blue-500 to-purple-600;
  @apply bg-clip-text text-transparent;
}

.gaming-button {
  @apply bg-gradient-to-r from-purple-600 to-cyan-600;
  @apply hover:from-purple-700 hover:to-cyan-700;
  @apply transform hover:-translate-y-1 transition-all duration-300;
  @apply shadow-lg hover:shadow-cyan-500/20;
}
```

---

## 🚀 Backend Gaming API

### **Architecture FastAPI**
```python
# Structure Backend
backend/
├── app/
│   ├── api/v1/
│   │   ├── endpoints/
│   │   │   ├── avatar.py          # Système avatars NFT
│   │   │   ├── marketplace.py     # Trading P2P
│   │   │   ├── cyba_coins.py     # Token economy
│   │   │   ├── gaming.py         # Mécaniques gaming
│   │   │   └── web3.py           # Intégrations blockchain
│   │   └── api.py
│   ├── models/
│   │   ├── avatar.py             # Modèles avatars gaming
│   │   ├── equipment.py          # Équipements NFT
│   │   ├── transactions.py       # Transactions CYBA
│   │   └── web3_integration.py   # Liens blockchain
│   ├── services/
│   │   ├── avatar_service.py     # Logique métier avatars
│   │   ├── marketplace_service.py # Marketplace P2P
│   │   ├── web3_service.py       # Interactions smart contracts
│   │   └── gaming_service.py     # Rewards et progression
│   └── core/
│       ├── security.py           # Sécurité Web3
│       ├── blockchain.py         # Utils blockchain
│       └── config.py
```

### **API Endpoints Gaming**

#### **Avatar Management**
```python
# endpoints/avatar.py
@router.get("/selection")
async def get_avatar_selection(user: User = Depends(get_current_user)):
    """Récupère avatars disponibles selon niveau utilisateur"""
    avatars = await avatar_service.get_available_avatars(user.level)
    return {
        "available_avatars": avatars,
        "user_level": user.level,
        "unlock_requirements": avatar_service.get_unlock_requirements()
    }

@router.post("/create")
async def create_user_avatar(
    avatar_data: AvatarCreateRequest,
    user: User = Depends(get_current_user)
):
    """Crée nouvel avatar utilisateur avec mint NFT"""
    # Vérification unlock level
    # Mint NFT sur blockchain si premium
    # Création avatar en base
    avatar = await avatar_service.create_avatar(user.id, avatar_data)
    return {"avatar": avatar, "nft_transaction": avatar.nft_tx_hash}
```

#### **Marketplace P2P**
```python
# endpoints/marketplace.py
@router.get("/equipment")
async def browse_marketplace(
    filters: MarketplaceFilters = Depends(),
    pagination: PaginationParams = Depends()
):
    """Browse équipements marketplace avec filtres"""
    equipment = await marketplace_service.get_equipment_listings(
        filters, pagination
    )
    return {
        "equipment": equipment,
        "total_count": len(equipment),
        "price_range": await marketplace_service.get_price_range()
    }

@router.post("/purchase")
async def purchase_equipment(
    purchase_data: EquipmentPurchaseRequest,
    user: User = Depends(get_current_user)
):
    """Achète équipement avec CYBA Coins"""
    # Vérification solde CYBA
    # Transaction blockchain si NFT
    # Ajout à inventaire utilisateur
    transaction = await marketplace_service.purchase_equipment(
        user.id, purchase_data
    )
    return {"transaction": transaction, "new_balance": user.cyba_balance}
```

### **Services Gaming**

#### **Avatar Service**
```python
# services/avatar_service.py
class AvatarService:
    def __init__(self, web3_service: Web3Service):
        self.web3 = web3_service
    
    async def create_avatar(self, user_id: int, avatar_data: AvatarCreateRequest):
        """Création avatar avec intégration blockchain"""
        
        # Vérification requirements
        if not await self.check_unlock_requirements(user_id, avatar_data.avatar_type):
            raise HTTPException(400, "Avatar not unlocked")
        
        # Mint NFT si avatar premium
        nft_tx = None
        if avatar_data.is_premium:
            nft_tx = await self.web3.mint_avatar_nft(
                user_id, avatar_data.avatar_type
            )
        
        # Création en base avec stats calculées
        avatar = UserAvatar(
            user_id=user_id,
            avatar_base_id=avatar_data.avatar_base_id,
            custom_name=avatar_data.custom_name,
            total_strength=self.calculate_total_stats(avatar_data),
            nft_token_id=nft_tx.token_id if nft_tx else None,
            is_active=True
        )
        
        return await self.repository.create(avatar)
    
    async def calculate_equipment_bonus(self, user_id: int) -> Dict[str, int]:
        """Calcule bonus total équipements équipés"""
        equipped_items = await self.get_equipped_items(user_id)
        bonus = {"strength": 0, "intelligence": 0, "agility": 0, "defense": 0, "luck": 0}
        
        for item in equipped_items:
            bonus["strength"] += item.strength_bonus
            bonus["intelligence"] += item.intelligence_bonus
            # etc...
            
        return bonus
```

---

## ⛓️ Smart Contracts Architecture

### **Contracts Principaux**

#### **CYBA Token (ERC-20)**
```solidity
// contracts/CYBAToken.sol
pragma solidity ^0.8.19;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/security/Pausable.sol";
import "@openzeppelin/contracts/access/AccessControl.sol";

contract CYBAToken is ERC20, Pausable, AccessControl {
    bytes32 public constant MINTER_ROLE = keccak256("MINTER_ROLE");
    bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
    
    uint256 public constant MAX_SUPPLY = 1_000_000_000 * 10**18; // 1B CYBA
    
    mapping(address => uint256) private _stakingBalance;
    mapping(address => uint256) private _stakingTimestamp;
    
    event TokensStaked(address indexed user, uint256 amount);
    event TokensUnstaked(address indexed user, uint256 amount, uint256 rewards);
    
    constructor() ERC20("CYBA Token", "CYBA") {
        _grantRole(DEFAULT_ADMIN_ROLE, msg.sender);
        _grantRole(MINTER_ROLE, msg.sender);
        _grantRole(PAUSER_ROLE, msg.sender);
        
        // Mint initial supply pour distribution
        _mint(msg.sender, 50_000_000 * 10**18); // 50M pour liquidity
    }
    
    function mintRewards(address to, uint256 amount) 
        public onlyRole(MINTER_ROLE) whenNotPaused {
        require(totalSupply() + amount <= MAX_SUPPLY, "Max supply exceeded");
        _mint(to, amount);
    }
    
    function stakeTokens(uint256 amount) external whenNotPaused {
        require(balanceOf(msg.sender) >= amount, "Insufficient balance");
        require(amount > 0, "Amount must be > 0");
        
        // Unstake previous si existant
        if (_stakingBalance[msg.sender] > 0) {
            unstakeTokens();
        }
        
        _transfer(msg.sender, address(this), amount);
        _stakingBalance[msg.sender] = amount;
        _stakingTimestamp[msg.sender] = block.timestamp;
        
        emit TokensStaked(msg.sender, amount);
    }
    
    function unstakeTokens() public whenNotPaused {
        uint256 stakedAmount = _stakingBalance[msg.sender];
        require(stakedAmount > 0, "No tokens staked");
        
        // Calcul rewards (8% APY base)
        uint256 stakingDuration = block.timestamp - _stakingTimestamp[msg.sender];
        uint256 rewards = (stakedAmount * 8 * stakingDuration) / (365 days * 100);
        
        _stakingBalance[msg.sender] = 0;
        _stakingTimestamp[msg.sender] = 0;
        
        // Transfer staked + rewards
        _transfer(address(this), msg.sender, stakedAmount);
        if (rewards > 0 && totalSupply() + rewards <= MAX_SUPPLY) {
            _mint(msg.sender, rewards);
        }
        
        emit TokensUnstaked(msg.sender, stakedAmount, rewards);
    }
    
    function getStakingInfo(address user) external view returns (
        uint256 stakedAmount,
        uint256 stakingDuration,
        uint256 estimatedRewards
    ) {
        stakedAmount = _stakingBalance[user];
        if (stakedAmount > 0) {
            stakingDuration = block.timestamp - _stakingTimestamp[user];
            estimatedRewards = (stakedAmount * 8 * stakingDuration) / (365 days * 100);
        }
    }
}
```

#### **CYBA Avatars NFT (ERC-721)**
```solidity
// contracts/CYBAAvatars.sol
pragma solidity ^0.8.19;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/security/ReentrancyGuard.sol";
import "@openzeppelin/contracts/security/Pausable.sol";
import "@openzeppelin/contracts/access/AccessControl.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract CYBAAvatars is ERC721, ReentrancyGuard, Pausable, AccessControl {
    using Counters for Counters.Counter;
    
    bytes32 public constant MINTER_ROLE = keccak256("MINTER_ROLE");
    bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
    
    Counters.Counter private _tokenIds;
    uint256 public constant MAX_SUPPLY = 10000;
    string private _baseTokenURI;
    
    enum AvatarType {
        CYBER_ROOKIE,
        HACKER_ELITE, 
        CYBER_GUARDIAN,
        MATRIX_WARRIOR,
        GHOST_OPERATIVE,
        DATA_MYSTIC,
        QUANTUM_ENGINEER,
        CYBORG_LEGEND
    }
    
    struct AvatarStats {
        AvatarType avatarType;
        uint8 strength;
        uint8 intelligence;
        uint8 agility;
        uint8 defense;
        uint8 luck;
        uint8 rarity; // 1-7 (Common to Cosmic)
        uint256 experience;
        bool isGenesis;
        uint256 mintTimestamp;
    }
    
    mapping(uint256 => AvatarStats) public avatarStats;
    mapping(AvatarType => uint256) public avatarTypeCount;
    mapping(address => uint256[]) public userAvatars;
    
    event AvatarMinted(
        address indexed to,
        uint256 indexed tokenId,
        AvatarType avatarType,
        uint8 rarity
    );
    
    event AvatarLevelUp(
        uint256 indexed tokenId,
        uint256 oldExperience,
        uint256 newExperience
    );
    
    constructor(string memory baseURI) ERC721("CYBA Avatars", "CYBA") {
        _baseTokenURI = baseURI;
        _grantRole(DEFAULT_ADMIN_ROLE, msg.sender);
        _grantRole(MINTER_ROLE, msg.sender);
        _grantRole(PAUSER_ROLE, msg.sender);
    }
    
    function safeMint(
        address to,
        AvatarType avatarType,
        AvatarStats memory stats
    ) public onlyRole(MINTER_ROLE) nonReentrant whenNotPaused {
        require(_tokenIds.current() < MAX_SUPPLY, "Max supply reached");
        require(to != address(0), "Cannot mint to zero address");
        
        _tokenIds.increment();
        uint256 tokenId = _tokenIds.current();
        
        // Set avatar stats
        avatarStats[tokenId] = AvatarStats({
            avatarType: avatarType,
            strength: stats.strength,
            intelligence: stats.intelligence,
            agility: stats.agility,
            defense: stats.defense,
            luck: stats.luck,
            rarity: stats.rarity,
            experience: 0,
            isGenesis: true,
            mintTimestamp: block.timestamp
        });
        
        avatarTypeCount[avatarType]++;
        userAvatars[to].push(tokenId);
        
        _safeMint(to, tokenId);
        
        emit AvatarMinted(to, tokenId, avatarType, stats.rarity);
    }
    
    function addExperience(uint256 tokenId, uint256 xpGain) 
        external onlyRole(MINTER_ROLE) {
        require(_exists(tokenId), "Avatar does not exist");
        
        AvatarStats storage avatar = avatarStats[tokenId];
        uint256 oldXp = avatar.experience;
        avatar.experience += xpGain;
        
        emit AvatarLevelUp(tokenId, oldXp, avatar.experience);
    }
    
    function getAvatarsByOwner(address owner) 
        external view returns (uint256[] memory) {
        return userAvatars[owner];
    }
    
    function getAvatarStats(uint256 tokenId) 
        external view returns (AvatarStats memory) {
        require(_exists(tokenId), "Avatar does not exist");
        return avatarStats[tokenId];
    }
    
    function _baseURI() internal view override returns (string memory) {
        return _baseTokenURI;
    }
    
    function setBaseURI(string memory baseURI) 
        external onlyRole(DEFAULT_ADMIN_ROLE) {
        _baseTokenURI = baseURI;
    }
    
    function pause() public onlyRole(PAUSER_ROLE) {
        _pause();
    }
    
    function unpause() public onlyRole(PAUSER_ROLE) {
        _unpause();
    }
    
    // Override required par Solidity
    function supportsInterface(bytes4 interfaceId)
        public view override(ERC721, AccessControl) returns (bool) {
        return super.supportsInterface(interfaceId);
    }
}
```

#### **Marketplace P2P**
```solidity
// contracts/CYBAMarketplace.sol
pragma solidity ^0.8.19;

import "@openzeppelin/contracts/security/ReentrancyGuard.sol";
import "@openzeppelin/contracts/security/Pausable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/token/ERC721/IERC721.sol";
import "@openzeppelin/contracts/token/ERC20/IERC20.sol";

contract CYBAMarketplace is ReentrancyGuard, Pausable, Ownable {
    IERC20 public cybaToken;
    
    uint256 public marketplaceFee = 250; // 2.5%
    uint256 public constant MAX_FEE = 1000; // 10% max
    
    struct Listing {
        address seller;
        address nftContract;
        uint256 tokenId;
        uint256 price; // Prix en CYBA tokens
        bool active;
        uint256 expiresAt;
        uint256 createdAt;
    }
    
    mapping(bytes32 => Listing) public listings;
    mapping(address => uint256[]) public userListings;
    
    event ListingCreated(
        bytes32 indexed listingId,
        address indexed seller,
        address indexed nftContract,
        uint256 tokenId,
        uint256 price,
        uint256 expiresAt
    );
    
    event NFTSold(
        bytes32 indexed listingId,
        address indexed seller,
        address indexed buyer,
        uint256 price,
        uint256 fee
    );
    
    event ListingCancelled(bytes32 indexed listingId);
    
    constructor(address _cybaToken) {
        cybaToken = IERC20(_cybaToken);
    }
    
    function createListing(
        address nftContract,
        uint256 tokenId,
        uint256 price,
        uint256 duration
    ) external nonReentrant whenNotPaused {
        require(price > 0, "Price must be > 0");
        require(duration > 0 && duration <= 30 days, "Invalid duration");
        
        IERC721 nft = IERC721(nftContract);
        require(nft.ownerOf(tokenId) == msg.sender, "Not token owner");
        require(nft.isApprovedForAll(msg.sender, address(this)) || 
                nft.getApproved(tokenId) == address(this), "Not approved");
        
        bytes32 listingId = keccak256(abi.encode(
            nftContract, tokenId, msg.sender, block.timestamp
        ));
        
        listings[listingId] = Listing({
            seller: msg.sender,
            nftContract: nftContract,
            tokenId: tokenId,
            price: price,
            active: true,
            expiresAt: block.timestamp + duration,
            createdAt: block.timestamp
        });
        
        userListings[msg.sender].push(uint256(listingId));
        
        emit ListingCreated(
            listingId, msg.sender, nftContract, tokenId, price, 
            block.timestamp + duration
        );
    }
    
    function buyNFT(bytes32 listingId) external nonReentrant whenNotPaused {
        Listing storage listing = listings[listingId];
        require(listing.active, "Listing not active");
        require(block.timestamp <= listing.expiresAt, "Listing expired");
        require(msg.sender != listing.seller, "Cannot buy own NFT");
        
        uint256 fee = (listing.price * marketplaceFee) / 10000;
        uint256 sellerAmount = listing.price - fee;
        
        require(cybaToken.balanceOf(msg.sender) >= listing.price, 
                "Insufficient CYBA balance");
        
        listing.active = false;
        
        // Transfer CYBA tokens
        require(cybaToken.transferFrom(msg.sender, address(this), fee),
                "Fee transfer failed");
        require(cybaToken.transferFrom(msg.sender, listing.seller, sellerAmount),
                "Payment transfer failed");
        
        // Transfer NFT
        IERC721(listing.nftContract).safeTransferFrom(
            listing.seller, msg.sender, listing.tokenId
        );
        
        emit NFTSold(listingId, listing.seller, msg.sender, listing.price, fee);
    }
    
    function cancelListing(bytes32 listingId) external {
        Listing storage listing = listings[listingId];
        require(listing.seller == msg.sender, "Not listing owner");
        require(listing.active, "Listing not active");
        
        listing.active = false;
        
        emit ListingCancelled(listingId);
    }
    
    function withdrawFees() external onlyOwner {
        uint256 balance = cybaToken.balanceOf(address(this));
        require(balance > 0, "No fees to withdraw");
        require(cybaToken.transfer(owner(), balance), "Transfer failed");
    }
    
    function updateMarketplaceFee(uint256 newFee) external onlyOwner {
        require(newFee <= MAX_FEE, "Fee too high");
        marketplaceFee = newFee;
    }
}
```

---

## 🎭 NFT Metadata & IPFS

### **Metadata Structure**
```json
{
  "name": "CYBA Cyber Rookie #1234",
  "description": "Apprenti Hacker avec laptop et détermination. Première génération des Cyber Warriors de CYBA Universe.",
  "image": "ipfs://QmXX...../avatar-cyber-rookie-1234.png",
  "external_url": "https://cyba-universe.com/avatar/1234",
  "attributes": [
    {
      "trait_type": "Avatar Type",
      "value": "Cyber Rookie"
    },
    {
      "trait_type": "Rarity",
      "value": "Genesis"
    },
    {
      "trait_type": "Strength",
      "value": 8,
      "max_value": 30
    },
    {
      "trait_type": "Intelligence", 
      "value": 12,
      "max_value": 30
    },
    {
      "trait_type": "Agility",
      "value": 10,
      "max_value": 30
    },
    {
      "trait_type": "Defense",
      "value": 8,
      "max_value": 30
    },
    {
      "trait_type": "Luck",
      "value": 12,
      "max_value": 30
    },
    {
      "trait_type": "Generation",
      "value": "Genesis"
    },
    {
      "trait_type": "Mint Date",
      "value": "2025-10-31",
      "display_type": "date"
    }
  ],
  "stats": {
    "total_power": 50,
    "experience": 0,
    "level": 1,
    "equipment_slots": 10
  },
  "gaming": {
    "combat_style": "Support Tactique",
    "signature_weapon": "Laptop de Combat",
    "special_abilities": ["Code Debug", "Tactical Analysis"],
    "lore": "Dans les profondeurs du cyberespace, un nouveau guerrier émerge..."
  }
}
```

---

## 🔒 Sécurité & Monitoring

### **Security Framework**
```yaml
🛡️ SECURITY LAYERS:
├── Smart Contract Security:
│   ├── OpenZeppelin base contracts
│   ├── Reentrancy guards
│   ├── Access control (RBAC)
│   ├── Pausable mechanisms
│   ├── Time locks
│   └── Multi-signature wallets
├── Economic Security:
│   ├── Rate limiting
│   ├── Price oracle protection
│   ├── Slippage protection
│   └── Treasury multisig
├── Operational Security:
│   ├── External audits (CertiK, ConsenSys)
│   ├── Bug bounty program
│   ├── 24/7 monitoring
│   └── Incident response plan
└── Data Security:
    ├── IPFS décentralisé
    ├── Metadata immutable
    ├── Backup redondant
    └── Privacy by design
```

### **Monitoring Dashboard**
```typescript
// monitoring/SecurityDashboard.tsx
interface SecurityMetrics {
  contractHealth: 'healthy' | 'warning' | 'critical';
  transactionVolume: number;
  gasOptimization: number;
  stakingRatio: number;
  liquidityHealth: number;
  anomalyDetection: Alert[];
}

export const SecurityDashboard = () => {
  const metrics = useSecurityMetrics();
  
  return (
    <div className="security-dashboard">
      <ContractHealthWidget health={metrics.contractHealth} />
      <TransactionMonitor volume={metrics.transactionVolume} />
      <GasOptimizer efficiency={metrics.gasOptimization} />
      <AnomalyAlerts alerts={metrics.anomalyDetection} />
    </div>
  );
};
```

---

## 🚀 Déploiement & Infrastructure

### **CI/CD Pipeline**
```yaml
# .github/workflows/deploy.yml
name: CYBA Universe Deployment
on:
  push:
    branches: [main]
    
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Smart Contract Tests
        run: |
          npm install
          npx hardhat test
          npx hardhat coverage
      
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Slither Analysis
        run: slither . --json slither-report.json
      - name: Mythril Scan
        run: myth analyze contracts/ --solv 0.8.19
        
  deploy-testnet:
    needs: [test, security-scan]
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Mumbai
        run: npx hardhat deploy --network mumbai
        
  deploy-mainnet:
    needs: [deploy-testnet]
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Polygon
        run: npx hardhat deploy --network polygon
```

### **Infrastructure as Code**
```yaml
# infrastructure/terraform/main.tf
resource "aws_ecs_cluster" "cyba_cluster" {
  name = "cyba-universe"
  
  setting {
    name  = "containerInsights"
    value = "enabled"
  }
}

resource "aws_ecs_service" "frontend" {
  name            = "cyba-frontend"
  cluster         = aws_ecs_cluster.cyba_cluster.id
  task_definition = aws_ecs_task_definition.frontend.arn
  desired_count   = 3
  
  load_balancer {
    target_group_arn = aws_lb_target_group.frontend.arn
    container_name   = "frontend"
    container_port   = 3000
  }
}

resource "aws_ecs_service" "backend" {
  name            = "cyba-backend"
  cluster         = aws_ecs_cluster.cyba_cluster.id
  task_definition = aws_ecs_task_definition.backend.arn
  desired_count   = 2
}
```

---

*Cette architecture technique garantit une plateforme gaming Web3 sécurisée, performante et scalable pour CYBA Universe ! 🚀*