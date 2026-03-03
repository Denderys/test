# test
-layer3
-OS
-MagicEden
-rbtn
-rubiscore
-humster
-twitter
Tempo node
#moderato
sudo apt update && sudo apt upgrade -y
sudo apt install curl wget git build-essential jq -y
##

##Revapay



--Dr?


#!/bin/bash

echo "Updating system..."
sudo apt update && sudo apt upgrade -y

echo "Installing dependencies..."
sudo apt install curl wget git docker.io docker-compose -y

sudo systemctl enable docker
sudo systemctl start docker

echo "Cloning Tempo repository..."
git clone https://github.com/tempo-network/tempo.git
cd tempo

echo "Starting node..."
docker compose up -d

echo "Tempo node installation completed!"

#serv param
2gb ram
Hetzner & contabo
## looking forward to growing with Axpha
## stock
googl 312.5



918 - 25.02 16.29
===========================

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/utils/Base64.sol";
import "@openzeppelin/contracts/utils/Strings.sol";

contract TxHistoryNFT is ERC721, Ownable {

    using Strings for uint256;

    uint256 public nextTokenId;
    uint256 public constant MAX_PER_WALLET = 5;
    bool public mintEnabled = true;

    struct TxData {
        uint256 txNumber;
        uint256 timestamp;
        uint256 blockNumber;
    }

    mapping(address => uint256) public txCount;
    mapping(uint256 => TxData) public txInfo;

    constructor() ERC721("TxHistoryNFT", "THN") Ownable(msg.sender) {}

    function mint() public {
        require(mintEnabled, "Mint disabled");
        require(txCount[msg.sender] < MAX_PER_WALLET, "Mint limit reached");

        txCount[msg.sender]++;
        nextTokenId++;

        _safeMint(msg.sender, nextTokenId);

        txInfo[nextTokenId] = TxData({
            txNumber: txCount[msg.sender],
            timestamp: block.timestamp,
            blockNumber: block.number
        });
    }

    function toggleMint() public onlyOwner {
        mintEnabled = !mintEnabled;
    }

    function tokenURI(uint256 tokenId) public view override returns (string memory) {
        require(_exists(tokenId), "Nonexistent token");

        TxData memory data = txInfo[tokenId];

        string memory svg = string(
            abi.encodePacked(
                '<svg xmlns="http://www.w3.org/2000/svg" width="500" height="500">',
                '<rect width="100%" height="100%" fill="black"/>',
                '<text x="50%" y="40%" dominant-baseline="middle" text-anchor="middle" fill="white" font-size="24">',
                'Tx NFT #', tokenId.toString(),
                '</text>',
                '<text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle" fill="white" font-size="18">',
                'Tx Number: ', data.txNumber.toString(),
                '</text>',
                '<text x="50%" y="60%" dominant-baseline="middle" text-anchor="middle" fill="white" font-size="16">',
                'Block: ', data.blockNumber.toString(),
                '</text>',
                '</svg>'
            )
        );

        string memory image = string(
            abi.encodePacked(
                "data:image/svg+xml;base64,",
                Base64.encode(bytes(svg))
            )
        );

        string memory metadata = string(
            abi.encodePacked(
                '{"name":"TxHistory NFT #', tokenId.toString(),
                '","description":"On-chain transaction history NFT",',
                '"image":"', image, '"}'
            )
        );

        return string(
            abi.encodePacked(
                "data:application/json;base64,",
                Base64.encode(bytes(metadata))
            )
        );
    }
}
============================

