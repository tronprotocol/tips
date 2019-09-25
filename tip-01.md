```
TIP: 0001
Title: Tron Wallet Proposal - Key Derivation Methods for Tron Accounts with BIP39
Author: getty.io
Created: 2017-04-05
```

## Simple Summary
This Tron Wallet Proposal describes methods for key derivation. This should improve key storage and moving keys between wallets and apps.

## Motivation
Currently the only way to store Tron account's keys is by saving a long str-encoded string which represents a secret key. However many industry standards have been developed for deriving keys which improve key storage and moving keys between wallets. Adapting these standards for Tron accounts should improve Tron wallets by:
* making key derivation the same across wallets and apps,
* allowing users to hold keys in hardware wallets,
* allowing users to hold keys in cold storage more reliably (using mnemonic codes),
* allowing users to generate multiple keys from a single seed (ex. first for storing funds and second as a signer for a shared account).

## Specification


### Multi-Account Hierarchy for Deterministic Wallets

We adapt [BIP-0044](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) for generating deterministic wallets, with `coin_type` equal `195` as assigned in [SLIP-0044](https://github.com/satoshilabs/slips/blob/master/slip-0044.md).

The following path should be used to generate accounts: `m/44'/195'/x'`. We call `m/44'/195'/0'` the _primary account_.

### Mnemonic Codes

[BIP-0039](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) should be used to derive binary seed from a mnemonic code.

We strongly recommend using 24 word mnemonic (256 bits of entropy).

## Rationale
`BIP`s are industry standards used by a majority of cryptocurrencies and software/hardware wallets.

We decided not to use the full derivation path specified in [BIP-0044](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) and follow the standard proposed by Stellar Lumens team [SEP-005](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0005.md)

## Test Cases

### Test 1
```
---------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/0'
Private Key: F43EBCC94E6C257EDBE559183D1A8778B2D5A08040902C0F0A77A3343A1D0EA5
Password = base64(Private Key):  9D68yU5sJX7b5VkYPRqHeLLVoIBAkCwPCnejNDodDqU=
Public Key: 04e6a49d098ee94871252622b8a8b727e5cdf81b7138e5ac16591887f6e8c10e881e4b4250fa8c87f5b29ad020216a9ffd0acf5995a627d6c70e4dd274c54c20bd
sha3 = SHA3(Public Key[1, 65)):  45c0f682e8a3d97968fa895ce11973395042ba3c0b52b4cdf4e15ea77818f275
Address = A0||sha3[12,32): :  A0E11973395042BA3C0B52B4CDF4E15EA77818F275
sha256_0 = SHA256(Address):  CD5D4A7E8BE869C00E17F8F7712F41DBE2DDBD4D8EC36A7280CD578863717084
sha256_1 = SHA256(sha256_0):  10AE21E887E8FE30C591A22A5F8BB20EB32B2A739486DC5F3810E00BBDB58C5C
checkSum = sha256_1[0, 4):  10AE21E8
addchecksum = address || checkSum:  A0E11973395042BA3C0B52B4CDF4E15EA77818F27510AE21E8
base58Address = Base58(addchecksum):  27jbj4qgTM1hvReST6hEa8Ep8RDo2AM8TJo
-----------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/1'
Private Key: 4E3428AEFF8347043A6677654284805C16BDEF59F040C2D84D62B2E399F9DE40
Password = base64(Private Key):  TjQorv+DRwQ6ZndlQoSAXBa971nwQMLYTWKy45n53kA=
Public Key: 044f1f569b6e9ce62dee4c7802f21ed63f34aa7c9164531745b3728a8773a871d74eb6708141050e7be882525a1aa617a6fd6935bc916deaf172708d771be80776
sha3 = SHA3(Public Key[1, 65)):  373bf2fde40dc5fb5caa0942495a6d9fd4055279bcdaf5bc02489a98ad71b277
Address = A0||sha3[12,32): :  A0495A6D9FD4055279BCDAF5BC02489A98AD71B277
sha256_0 = SHA256(Address):  0F02C9C105223A9C04B8455C4A771CF0D6BC135BED81F15D436020B1A93DA401
sha256_1 = SHA256(sha256_0):  B06E3C3D8D51335FE84703700982F04A89356B4B6F5CCEE0F9B9B079E66300C2
checkSum = sha256_1[0, 4):  B06E3C3D
addchecksum = address || checkSum:  A0495A6D9FD4055279BCDAF5BC02489A98AD71B277B06E3C3D
base58Address = Base58(addchecksum):  27VmNCSYoBu3Q8DtPauBBFXDz36JbFANEHr
-----------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/2'
Private Key: 12CEA7EC62D3CACBA306A57FF6A840FDF49F29619FFE4E3391D5C0BBA7D8847B
Password = base64(Private Key):  Es6n7GLTysujBqV/9qhA/fSfKWGf/k4zkdXAu6fYhHs=
Public Key: 04171170fba11bf4d6ddc16eacec950d955522a085741d148196b3328acac9d124e104fc71f9a83fbfe32d8279a7d8357790762b8db066986fea56d94ae38153c4
sha3 = SHA3(Public Key[1, 65)):  9b0690b6b0e413635e4a41e46ead1fbeea79bb93344086e67954070b9c55d81b
Address = A0||sha3[12,32): :  A06EAD1FBEEA79BB93344086E67954070B9C55D81B
sha256_0 = SHA256(Address):  0BC59F16AF4DC542E5F8BA9D901A7FAAC0CD7B64B72BE150F3612A96B8A5AC7F
sha256_1 = SHA256(sha256_0):  3F9E39F2BEE94E21AA8BAC3CF479E48881BD39A99B0AA2D9D0BD7164556CDCE2
checkSum = sha256_1[0, 4):  3F9E39F2
addchecksum = address || checkSum:  A06EAD1FBEEA79BB93344086E67954070B9C55D81B3F9E39F2
base58Address = Base58(addchecksum):  27ZAiGLrD1d6n1ywxN5aPkD3SeVtCnVVEjT
-----------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/3'
Private Key: 1615279A00E3921ECD5C6ACBC15F2C88773C0D5821719CF26E24BD17BDDDE6F7
Password = base64(Private Key):  FhUnmgDjkh7NXGrLwV8siHc8DVghcZzybiS9F73d5vc=
Public Key: 04b1617fc9bf6f8c64c40527e1a0f6ffa321e844052b9758aaa6d256e656c93efe8d36c2603a4ae30e8f7c8e9b5ba89e5fbd1fb83734654947ee87f4d8b0f806fa
sha3 = SHA3(Public Key[1, 65)):  392deeb280a64f6039ff7e92b10bbe2472e21dead74fb971ddcd716f227487c3
Address = A0||sha3[12,32): :  A0B10BBE2472E21DEAD74FB971DDCD716F227487C3
sha256_0 = SHA256(Address):  45E326626C4F57F95785273F77593FB49B779E4757BC9BB528B54058247541DB
sha256_1 = SHA256(sha256_0):  6A156DFCEB331FB1BCE4CC0E219ECDBB98F99D2F0E444B1EBCAB0608494CDDD4
checkSum = sha256_1[0, 4):  6A156DFC
addchecksum = address || checkSum:  A0B10BBE2472E21DEAD74FB971DDCD716F227487C36A156DFC
base58Address = Base58(addchecksum):  27fDeDEEMDqwg1eBVzGXnGBGwfaTxwe3C2P
-----------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/4'
Private Key: B2D787D694AE6C9C59D1AC4255A9938C4EFE3D828FC14E4FFA960770B334D528
Password = base64(Private Key):  steH1pSubJxZ0axCVamTjE7+PYKPwU5P+pYHcLM01Sg=
Public Key: 04f17f18ccbb976ae8cba2351afb2838a30e5d8808e6c1e2bb7ab015695dcf79737567768bc5c66a8c755beb4980591172b1ca652b09284bf0fcff8497e7d04415
sha3 = SHA3(Public Key[1, 65)):  fd9f275234fd7899d7e116441adba05dbbb66b63f440f5d627c8d177d624eb4d
Address = A0||sha3[12,32): :  A01ADBA05DBBB66B63F440F5D627C8D177D624EB4D
sha256_0 = SHA256(Address):  DF7715B2861625A87A2C4C593746856A36DA571FB1AA4B078F9E13218150BCE9
sha256_1 = SHA256(sha256_0):  E3C4727A996A2876773CDAC27C4D6B1E200E764F972A467E1C147B06B91EE82E
checkSum = sha256_1[0, 4):  E3C4727A
addchecksum = address || checkSum:  A01ADBA05DBBB66B63F440F5D627C8D177D624EB4DE3C4727A
base58Address = Base58(addchecksum):  27RXXDGrym8zF36X2RDKaNEh2fSnUKCqUgh
-----------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/5'
Private Key: 3AAC0B309BFBE402EC434C43A9F17EE15E270254BBF65CEB1C7C45223DB91C30
Password = base64(Private Key):  OqwLMJv75ALsQ0xDqfF+4V4nAlS79lzrHHxFIj25HDA=
Public Key: 04c5f15456cfbc0477fdad2e33f5c038cbd1768cd3c006b6acb561d37263cfcb88094580dd63db1d3648011251c8259091b9064f877e4dc55fbda88e156e3e6644
sha3 = SHA3(Public Key[1, 65)):  0513a19e4e569cf4322227fcf714af619f216e34f54070836f35589799072375
Address = A0||sha3[12,32): :  A0F714AF619F216E34F54070836F35589799072375
sha256_0 = SHA256(Address):  14A090D494E9D3D0F0D93E6E4D18921820AC4AA98C6D0057A2D67097B67B4009
sha256_1 = SHA256(sha256_0):  385CC557F70BAF2F80530F2B8F8CBCCE027B6A4EEA2446F2C70667A52ABB2631
checkSum = sha256_1[0, 4):  385CC557
addchecksum = address || checkSum:  A0F714AF619F216E34F54070836F35589799072375385CC557
base58Address = Base58(addchecksum):  27mbxDyti7KhNpVNdB2Hnmvz7VMuw8hZXMx
-----------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/6'
Private Key: 98522860D3067B4DE6B28011D92FC694A6BF1B5639738ECAF909523FCE422E68
Password = base64(Private Key):  mFIoYNMGe03msoAR2S/GlKa/G1Y5c47K+QlSP85CLmg=
Public Key: 04686720617bf9dd210e092893d62ab6671a9ca92f1463843c26342e9e49960423fca94910a14831b8cb0579341d4a884c3fee7fd2169915982fb5a0e6cd2cb5f0
sha3 = SHA3(Public Key[1, 65)):  ac18d8322a55a284026445a5125ae14e39e353ed662d147a4a04ad5ae299f280
Address = A0||sha3[12,32): :  A0125AE14E39E353ED662D147A4A04AD5AE299F280
sha256_0 = SHA256(Address):  21DD55F3A9134275CDEA35E3BE809E31F87AD0BD62B3A1A1C99A57A5227FBD49
sha256_1 = SHA256(sha256_0):  68BC5A9B7CAF96E3A449C050CA21898A998276FFF73AADC95261CB8B5132AFF0
checkSum = sha256_1[0, 4):  68BC5A9B
addchecksum = address || checkSum:  A0125AE14E39E353ED662D147A4A04AD5AE299F28068BC5A9B
base58Address = Base58(addchecksum):  27QkZaHePRpBLkkYPZxbXpVMcY2vLz263jQ
-----------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/7'
Private Key: FB1AA970A918F4188038C210A3B0202D241482B765322B44FCA2A75C2D53D1A7
Password = base64(Private Key):  +xqpcKkY9BiAOMIQo7AgLSQUgrdlMitE/KKnXC1T0ac=
Public Key: 049937bfdc13b9463d39addb05e93868641360b87fdc2f191b62f4f3faef5607ea38b938d8de9231ac5778226d6daa2e2a8b6fa76a6379a812c9864867f6071ca8
sha3 = SHA3(Public Key[1, 65)):  1f6f6f904c6c6ea9adc37a097938cba6418051dba047c358e150225a276555fe
Address = A0||sha3[12,32): :  A07938CBA6418051DBA047C358E150225A276555FE
sha256_0 = SHA256(Address):  39A332821CC75AFDFF8945C26D9DEC7642DE6E3639A3EB3B8E790814F58F0BDF
sha256_1 = SHA256(sha256_0):  E70822F96741825C9FD19EBF6A7CFB48C4D00C90E792A1F4A68C63A8A5C128C1
checkSum = sha256_1[0, 4):  E70822F9
addchecksum = address || checkSum:  A07938CBA6418051DBA047C358E150225A276555FEE70822F9
base58Address = Base58(addchecksum):  27a8ULomfbsyLNS4cCNsmcqndDr2BTnP36G
-----------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/8'
Private Key: 20F86540EE41717E716D30FE4ED899275F5E28B27466589140D41366E314E39D
Password = base64(Private Key):  IPhlQO5BcX5xbTD+TtiZJ19eKLJ0ZliRQNQTZuMU450=
Public Key: 04f0b4aa5ff548476738ed8d4bf73f7d42479f08c7531596c6ad441a4e409a04e427873d41a0d196ea00c297d1a5b6966b153be3fdf7691c5ddf03355571418af7
sha3 = SHA3(Public Key[1, 65)):  0d54191fcf6fe89f872eb7390e8bc3cda46063061cbc59b3a52b7aabe7171560
Address = A0||sha3[12,32): :  A00E8BC3CDA46063061CBC59B3A52B7AABE7171560
sha256_0 = SHA256(Address):  1D87E010B93492889E0C913FB82E2BA3878CE749E856B48B828558E597366FB6
sha256_1 = SHA256(sha256_0):  525CC968AEC2E9EF1E2CA5FFD080FABF5E5DC35AD4C4A710ED71CDF4FA103239
checkSum = sha256_1[0, 4):  525CC968
addchecksum = address || checkSum:  A00E8BC3CDA46063061CBC59B3A52B7AABE7171560525CC968
base58Address = Base58(addchecksum):  27QQRS6Lp8ph3rK9YsKjHfUPgo66R368SSK
-----------------------------------------------------------------
Mnemonic (0 words):  00000000000000000000000000000000
BIP39 Seed:  7cc00a1be98ba277b3e1640cabe994cf4dc5142bcf9a3bb4cdf7027356a08af3e5aabe0199e89e439313ddbdcb16e205e364b6e1519e4b0a4448b06a846ad4bb
BIP39 Path:  m/44'/195'/9'
Private Key: 284A9C9A0CC4078E38A0BA90944A4F740BB49F8EFEC5A57ED79B00D6AF39B2D9
Password = base64(Private Key):  KEqcmgzEB444oLqQlEpPdAu0n47+xaV+15sA1q85stk=
Public Key: 0436403ec46ca1b1bd550f96d43fc71d95556ff6af23cbda545211429243d5480fffc9d9d731a113ab3f444fa80b3c87a1a5e98bec56d54bfc2752305cc4794132
sha3 = SHA3(Public Key[1, 65)):  bc45ee41352ec26e51fd6ec269a6b8e12b2f7ccded080fecd8a1a5700929de65
Address = A0||sha3[12,32): :  A069A6B8E12B2F7CCDED080FECD8A1A5700929DE65
sha256_0 = SHA256(Address):  363E3104B8825400EB29FE401F46E4848A06912E76C81FA09B59A6566147966E
sha256_1 = SHA256(sha256_0):  70C3C5B6F0C22B7F7E68DDECFEE8341692EFBD1838EE69555C111BDD5BA646A8
checkSum = sha256_1[0, 4):  70C3C5B6
addchecksum = address || checkSum:  A069A6B8E12B2F7CCDED080FECD8A1A5700929DE6570C3C5B6
base58Address = Base58(addchecksum):  27Yi9DaT8jfx3G9X8cn779DWgBYr2ZWVmeu
-----------------------------------------------------------------

```

### Test 2
```
---------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/0'
Private Key: 7CE4CA1A353AC69BAD43EEA9E2A1431655826495CB6921AFF0E3BFFC40B9CC19
Password = base64(Private Key):  fOTKGjU6xputQ+6p4qFDFlWCZJXLaSGv8OO//EC5zBk=
Public Key: 046893ece330e7889609a3d472034095e45bb62d60d3b9ab5953b9c6c23bbd16546fb700260b0e08821ac366ea5f8a8ac39e45d4a2d7c122527e83e0bcb51b54e8
sha3 = SHA3(Public Key[1, 65)):  3c8b0d6c9b4a6fe21f7b8b4ff63ec88f379255c32a67dc8d2961b1dbbcf3aefe
Address = A0||sha3[12,32): :  A0F63EC88F379255C32A67DC8D2961B1DBBCF3AEFE
sha256_0 = SHA256(Address):  033DA8AEE5C72AC20AB15D2574156CF2AA1A2ADDBAB863FBEF72E5325B83D097
sha256_1 = SHA256(sha256_0):  E990D2553F25C2B36217224BFBF39A04933291C484E0D98DB1F547F734B08877
checkSum = sha256_1[0, 4):  E990D255
addchecksum = address || checkSum:  A0F63EC88F379255C32A67DC8D2961B1DBBCF3AEFEE990D255
base58Address = Base58(addchecksum):  27mXXyqN1sA8AZW1v5zEP1fXRSz6eA4AMaL
-----------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/1'
Private Key: 76CBCBC004E3D8C2BD6BB91168AC8FF14615D846D15E07C1837DA3410FF013DE
Password = base64(Private Key):  dsvLwATj2MK9a7kRaKyP8UYV2EbRXgfBg32jQQ/wE94=
Public Key: 0472d3e4254b126ee7ef47e58b9407e073e9a2935d4442667859278333dab9e2bdd29366e5be98cdb47b46f56756d03b32157aaf646fbf42b868f65e9b0d98e50b
sha3 = SHA3(Public Key[1, 65)):  545613b8512486dc3e3a106b90b2c2d45e7d674a8e072af7b92cdcd9d914ef72
Address = A0||sha3[12,32): :  A090B2C2D45E7D674A8E072AF7B92CDCD9D914EF72
sha256_0 = SHA256(Address):  85AF63F4CFA27690311A45352EF1B45964E3931CE4853F83C042AFAE460219F0
sha256_1 = SHA256(sha256_0):  47E8EBF71B6E6CC719F208AAEE4B48CEEF76A4CC857E1F59DFAE659A675C244A
checkSum = sha256_1[0, 4):  47E8EBF7
addchecksum = address || checkSum:  A090B2C2D45E7D674A8E072AF7B92CDCD9D914EF7247E8EBF7
base58Address = Base58(addchecksum):  27cGbzXvwq1KzFcq3nKP9L3mGu8JEko5fVg
-----------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/2'
Private Key: 7FE066B9816B5F4FCD2C9C57EC97CB4F533DED027C3DC650A205E4B1BDB4BD30
Password = base64(Private Key):  f+BmuYFrX0/NLJxX7JfLT1M97QJ8PcZQogXksb20vTA=
Public Key: 0485ae062fef1d953fc6c4fca23f65d8825f1120dff4db754bb98de20fe84df96e8b43017507ad1eb277cb53e6e8ad0361d7e4eca050a550c82b9fe1b11adc1093
sha3 = SHA3(Public Key[1, 65)):  e7e5d69d27209d65b9f6193f4909942015988fff4d08b824f5b5be961ef90bf4
Address = A0||sha3[12,32): :  A04909942015988FFF4D08B824F5B5BE961EF90BF4
sha256_0 = SHA256(Address):  E1C5DB07FF645030ADE4870720E71849A516DFC07310BC8BADC4A845375A6E7A
sha256_1 = SHA256(sha256_0):  2CA601EEE1C0B4C8635206F5251060F6E1FD3DCFA61BA8849CF5325664666E9B
checkSum = sha256_1[0, 4):  2CA601EE
addchecksum = address || checkSum:  A04909942015988FFF4D08B824F5B5BE961EF90BF42CA601EE
base58Address = Base58(addchecksum):  27VjhLus1LgP3PkmMFxRbUGfP8UkJ9nVaLD
-----------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/3'
Private Key: 4DF12E81F3F2BEC254BC52516B88BD4F49FBDE532227BCC2B4CC0EACB9CFE1B7
Password = base64(Private Key):  TfEugfPyvsJUvFJRa4i9T0n73lMiJ7zCtMwOrLnP4bc=
Public Key: 0482677309614ce5a9e9a831f139b14c1251367f0535c7e90e5b8706c40bbbaa7dced1529bb4979ae61d21ee890385e9e1000d8fa4d6d7685c51383a4e0c21583e
sha3 = SHA3(Public Key[1, 65)):  0356bb15438ae211b2cc2b3ca326278e9199c37374ac0a0fd5545673f212600e
Address = A0||sha3[12,32): :  A0A326278E9199C37374AC0A0FD5545673F212600E
sha256_0 = SHA256(Address):  18DFAEFA5A210473B995766AE60F07E535B9FBFACB4E7C4530FD69F4B57E82C2
sha256_1 = SHA256(sha256_0):  06C2A43B6BB2D2724591C9508A49BE334EDE9037075FEBD58AD567FD196B4CA5
checkSum = sha256_1[0, 4):  06C2A43B
addchecksum = address || checkSum:  A0A326278E9199C37374AC0A0FD5545673F212600E06C2A43B
base58Address = Base58(addchecksum):  27dxAPfZSJstKHBGU4Em6wXRivZXfn736Kc
-----------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/4'
Private Key: 9C121E3348580E17163A0EEFD587B0231AC83E4181050DACF15C0FBCB478AB1E
Password = base64(Private Key):  nBIeM0hYDhcWOg7v1YewIxrIPkGBBQ2s8VwPvLR4qx4=
Public Key: 040764992b39935649fef6e55834306e69bfaa9e353aafee624a54f24d426ba60fe9f55c0a24e12b0f0298342a5b9fc6cd8c5885275808225dd6fe85a10e1281bb
sha3 = SHA3(Public Key[1, 65)):  f6290559f3a0bf02d3c481c3113fad54bf6312723d7881e6649a10ded2aa2279
Address = A0||sha3[12,32): :  A0113FAD54BF6312723D7881E6649A10DED2AA2279
sha256_0 = SHA256(Address):  1377A09644C4D130ACA41B776610CA29F39280CADFBB5CB217E4CF2080818012
sha256_1 = SHA256(sha256_0):  35CA4E161E3B12FAA9865959D8AE06169F9A709B917E4F8272F66C8FA34A214E
checkSum = sha256_1[0, 4):  35CA4E16
addchecksum = address || checkSum:  A0113FAD54BF6312723D7881E6649A10DED2AA227935CA4E16
base58Address = Base58(addchecksum):  27QeiJzksGsxVFGGeM6VgYvV3dShrBcRPem
-----------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/5'
Private Key: 7E7629D4636CB71D0092C4B10B88A55C74955C12FC850530805568E397AF4024
Password = base64(Private Key):  fnYp1GNstx0AksSxC4ilXHSVXBL8hQUwgFVo45evQCQ=
Public Key: 04a725fdfeb980b09171b1f197e1686fe9398e927462b157b3f87e482eef48ec5143ad255f65576186ea98adf2f6ff2c786970a7117693cfbfdee89b88a188fe1e
sha3 = SHA3(Public Key[1, 65)):  4ed5c669a3ca1e48bf8ceb2ec4accde348fca82ec9fb3799935f70490e6e295a
Address = A0||sha3[12,32): :  A0C4ACCDE348FCA82EC9FB3799935F70490E6E295A
sha256_0 = SHA256(Address):  BAE0ED9C09A441A7846CFA0858D867299291072ADC72BA4E21246BB161BB9F7F
sha256_1 = SHA256(sha256_0):  2DD0251B6180D919A7342B21907D82C75300CF67B44AA286D4E1701E5D4B92DA
checkSum = sha256_1[0, 4):  2DD0251B
addchecksum = address || checkSum:  A0C4ACCDE348FCA82EC9FB3799935F70490E6E295A2DD0251B
base58Address = Base58(addchecksum):  27h1Rzd73Sd7Hqzxx3PNN5e7dH5eAoHbw8W
-----------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/6'
Private Key: 0796F331557ECBD3095B16FF75B7A4A8BC0667D29A4FFC9284460903CD34A5BF
Password = base64(Private Key):  B5bzMVV+y9MJWxb/dbekqLwGZ9KaT/yShEYJA800pb8=
Public Key: 042c29e3aa4c7a8ee59175de5465ded59573a17f8579e892d94b5be7a61db161d1f709e50e540887fb181de07eb1a7c0b65c30568bcc43a2b8d2a79d7c47992a4c
sha3 = SHA3(Public Key[1, 65)):  27de6e37df27573b920a66bb2f78efdf89660e1d57d80f4ca2808285265d1862
Address = A0||sha3[12,32): :  A02F78EFDF89660E1D57D80F4CA2808285265D1862
sha256_0 = SHA256(Address):  3EE37EB1F9142E59ED98E95DE4DC46544379CD26E5FA44A1BC85AF95CC1EF3F9
sha256_1 = SHA256(sha256_0):  98262314E7E379FEA4FDEF1B39991AF20B7A02181D886DFFF6E3171D9D9028BA
checkSum = sha256_1[0, 4):  98262314
addchecksum = address || checkSum:  A02F78EFDF89660E1D57D80F4CA2808285265D186298262314
base58Address = Base58(addchecksum):  27TQXBEwkSohYZZXGdWvEXXc3C8XMP2h1Xy
-----------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/7'
Private Key: 3A661657210E1FEF2468D59E87C896F68C14F6315CDE04E1C688B1C9566CB7A9
Password = base64(Private Key):  OmYWVyEOH+8kaNWeh8iW9owU9jFc3gThxoixyVZst6k=
Public Key: 044a8d07b5d58f0b8b58cf5fa87b31fe3e059ba662240670f3b57787920519815154a35c612bd0121a63fe11b857340e6d3abffdea7e369f12c0513f21618dbcdd
sha3 = SHA3(Public Key[1, 65)):  29109e3bb89f695f139f1b08e454bbff8b7657306c111aebb7e1b9e97c1ac7dc
Address = A0||sha3[12,32): :  A0E454BBFF8B7657306C111AEBB7E1B9E97C1AC7DC
sha256_0 = SHA256(Address):  B6E5456A272CF0CE8751D5375B9E917D43B53C2D39066F36C28DF302B552AB51
sha256_1 = SHA256(sha256_0):  A63EF2220C6869903F4D7E6E423C941588DF3CFCF494CAC2E28BAA4EBA7FB966
checkSum = sha256_1[0, 4):  A63EF222
addchecksum = address || checkSum:  A0E454BBFF8B7657306C111AEBB7E1B9E97C1AC7DCA63EF222
base58Address = Base58(addchecksum):  27jtp7ZPZSJbexbYHouRxHwjK2J6Zx7vhXo
-----------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/8'
Private Key: 552E243A99A9F0A3DFF1FFB62F121BB702B6F06557FDDEF39A7F867327080B7E
Password = base64(Private Key):  VS4kOpmp8KPf8f+2LxIbtwK28GVX/d7zmn+GcycIC34=
Public Key: 041ae3a73506d4a79e05ce547c4e3f0643c3721a7df2a2d60a3ccf16a9432a1579de52399f3b4e771d6cb832420a59ee81cccf1233d5f4ca0ef7f2619307e7ba7b
sha3 = SHA3(Public Key[1, 65)):  a0e78252104e9625fc593a2a70e22436917f16218d712f0aa17b3dff82781ab1
Address = A0||sha3[12,32): :  A070E22436917F16218D712F0AA17B3DFF82781AB1
sha256_0 = SHA256(Address):  C0E63493CBDC822BA8E825E16C8C671F2E0B108F5B6A6C5EDE673B34102ADA71
sha256_1 = SHA256(sha256_0):  B87BBC3C99FBC1CC76A29D3AA0216A70D7079DABC3BB2439801A734EDC96A8B8
checkSum = sha256_1[0, 4):  B87BBC3C
addchecksum = address || checkSum:  A070E22436917F16218D712F0AA17B3DFF82781AB1B87BBC3C
base58Address = Base58(addchecksum):  27ZNP8Sh2UwM98GFSWT2rw3kfFDeZQW1fdD
-----------------------------------------------------------------
Mnemonic (12 words):  ceiling present easily example nurse silver ecology plug accident decrease special aware
BIP39 Seed:  e0977fc24a90cf457a12c3e074e337abefa2efab4646324a20c80c9308bc19f1be4cab879f6b7644841f3a2076b65421fca6eae42200b8b6e72efdb471ff4ac5
BIP39 Path:  m/44'/195'/9'
Private Key: 37028745CB9474DB0B40C05B9B4834EC446EDF196EF0133B6B3936CAC94FF1DB
Password = base64(Private Key):  NwKHRcuUdNsLQMBbm0g07ERu3xlu8BM7azk2yslP8ds=
Public Key: 043e4eb672981b48f525f1d4bad04660d180cdab521f3652f8180ba9c909031fa4aa826f1652e9c1376e34883d392070117650d5080201e843d4cbea5621cc5dd6
sha3 = SHA3(Public Key[1, 65)):  19b7795898bcd420a0751c6524ad263cc9c25b3e538b07a7138a025f85f1e353
Address = A0||sha3[12,32): :  A024AD263CC9C25B3E538B07A7138A025F85F1E353
sha256_0 = SHA256(Address):  BE6AE3399E6A534B9685EFC084AB7BDAEBD81C4D5BC437CF25727B4B6B0B91EE
sha256_1 = SHA256(sha256_0):  1D622B171D38156F650AEE2649F951EBAB9A84D935C12972860259646C25ECBE
checkSum = sha256_1[0, 4):  1D622B17
addchecksum = address || checkSum:  A024AD263CC9C25B3E538B07A7138A025F85F1E3531D622B17
base58Address = Base58(addchecksum):  27SRSHuho47iKHSbZwCLChHQYbW4aP4EvgN
-----------------------------------------------------------------


```

### Test 3
```
---------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/0'
Private Key: A56A899E3B58B06B40E64CFD0EEA590A9FB377A27F4CBDF1FBC07AF92C5E74DD
Password = base64(Private Key):  pWqJnjtYsGtA5kz9DupZCp+zd6J/TL3x+8B6+SxedN0=
Public Key: 0401fafbde4dd825c88d791e256a45c443dd2e9e77f9be43fe5e0e6e4c81388e5f11be1f9b9f3f45ac549699e6b83e2eaa69a895ac65891524e383b67e6d9af93f
sha3 = SHA3(Public Key[1, 65)):  51252231784afaa43c2db6d8fdba61c13075795dcd6138eb2892d47e61b17938
Address = A0||sha3[12,32): :  A0FDBA61C13075795DCD6138EB2892D47E61B17938
sha256_0 = SHA256(Address):  F9226E31ECB6F62989E1DCF09227D4990426A37643DE0ABE690D854972F5E0D3
sha256_1 = SHA256(sha256_0):  2A5FC059528E4C72592F7E7F2FCEA1441C396B6D25D25F41C4D5D3C38C8B7A75
checkSum = sha256_1[0, 4):  2A5FC059
addchecksum = address || checkSum:  A0FDBA61C13075795DCD6138EB2892D47E61B179382A5FC059
base58Address = Base58(addchecksum):  27nD6mwq7LLGLzLxAaeALjxvkpqgvih2JXa
-----------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/1'
Private Key: 3ECD54468006617E7DC64C3DCD39E0F94BAEFAFCDD88335E90C16E973B837A26
Password = base64(Private Key):  Ps1URoAGYX59xkw9zTng+Uuu+vzdiDNekMFulzuDeiY=
Public Key: 0487c1a7fb73b432415d402711d2e3e1ffc12ea08ed32cf22919f66e908d97186ec635bc06fc38705414b90e364a5afed06767132d143bdb10441789d8416589e1
sha3 = SHA3(Public Key[1, 65)):  387ac671ae7b0aba08c61de03c67b0d75a39f05b5d9e951519197d90ae904381
Address = A0||sha3[12,32): :  A03C67B0D75A39F05B5D9E951519197D90AE904381
sha256_0 = SHA256(Address):  D0F9CA5014412B534AB201E31F321721BA9EB26FEDAA2A69F25BCF43C74CC00D
sha256_1 = SHA256(sha256_0):  3A6F47445354A4D8D9F96BCDDCCD5715AED303D3B78A08A9E794700FB3495FA3
checkSum = sha256_1[0, 4):  3A6F4744
addchecksum = address || checkSum:  A03C67B0D75A39F05B5D9E951519197D90AE9043813A6F4744
base58Address = Base58(addchecksum):  27UauJSs7NmAGZ3aW53MqYYT64SYcANaTB1
-----------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/2'
Private Key: 8D376E1F14CE4C32B58F89AACB283809047B3C5FDF075AB505334BA7EAC03DEB
Password = base64(Private Key):  jTduHxTOTDK1j4mqyyg4CQR7PF/fB1q1BTNLp+rAPes=
Public Key: 04d30ed783051867c94a9184304fec2d6110a564d776c19e019d3901ed6e187f409d1477170723cca1d6700ae7a2ddb22363f126bd9558dfe2cd555f0e87dc41ac
sha3 = SHA3(Public Key[1, 65)):  2dc8e2bed7d229d3ae7ba3330489e2102aef05ceaffe65e186f4d09b2e53246f
Address = A0||sha3[12,32): :  A00489E2102AEF05CEAFFE65E186F4D09B2E53246F
sha256_0 = SHA256(Address):  64596700CDAD3BC67E4B4F2BD135B716EE5E9636C3F0E97BDBDA64B260A3BA57
sha256_1 = SHA256(sha256_0):  6D3BF10FD27B69E6C727F2B2576AD7D0E691AF0D42E0E81BE0545FA7198E91F6
checkSum = sha256_1[0, 4):  6D3BF10F
addchecksum = address || checkSum:  A00489E2102AEF05CEAFFE65E186F4D09B2E53246F6D3BF10F
base58Address = Base58(addchecksum):  27PVWRRc4ndivbTpsxqfk99hWbWvELFsdav
-----------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/3'
Private Key: 4302709485C419E1B331575D7F45CF7AF430C2F103237DF7D768E89008E7B44A
Password = base64(Private Key):  QwJwlIXEGeGzMVddf0XPevQwwvEDI33312jokAjntEo=
Public Key: 04b08f7d898bb1b026ff9ae2474f3297503ece141f361bc54985309e57104a2b26c1cfa2c881747cdbcaf4e405f747cd6df8121823bb6777260a5b3825198fbf70
sha3 = SHA3(Public Key[1, 65)):  a13c3ac0050e212ab85c03e1a4e4a0f53e04efb0f0ab0f7dc5b1c53f9707678c
Address = A0||sha3[12,32): :  A0A4E4A0F53E04EFB0F0AB0F7DC5B1C53F9707678C
sha256_0 = SHA256(Address):  743C0DDCDF6F996CAEF172EEC2822F4AB3B47393C31B1DD2536C00B646CC14A7
sha256_1 = SHA256(sha256_0):  AD5AA804899517EDAAD6FB8E8BFFD356B3DA0984F5FBFB9FDF1CBB629CA68945
checkSum = sha256_1[0, 4):  AD5AA804
addchecksum = address || checkSum:  A0A4E4A0F53E04EFB0F0AB0F7DC5B1C53F9707678CAD5AA804
base58Address = Base58(addchecksum):  27e7PFEnWtNCzrNhRs1AZb1uZHxoiCzor27
-----------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/4'
Private Key: 1FE4572FE445551FA55B058FA3354BBA326AC5EF47735C2F5382B105C2ED1379
Password = base64(Private Key):  H+RXL+RFVR+lWwWPozVLujJqxe9Hc1wvU4KxBcLtE3k=
Public Key: 040d176512c2609996501e84d18951ff874d388fc1447115a93a23f46df4166d5ef180a999a2fac1ef03bb533073148eddbfba6cc630c4f51c5ab7e377bdcd504c
sha3 = SHA3(Public Key[1, 65)):  d4ab696d571fba904f9ca198da40031c5b7895c5c9cefe211f8d8f0b81cc65d6
Address = A0||sha3[12,32): :  A0DA40031C5B7895C5C9CEFE211F8D8F0B81CC65D6
sha256_0 = SHA256(Address):  05A479B4A4E84C6653D7975B03547A5ABFBBEBE9C405FB3200DF4466ED0E26F5
sha256_1 = SHA256(sha256_0):  CED66DE6BC750C2266064C1600F131541C6A0135B16C5D54198AAE1EC761864F
checkSum = sha256_1[0, 4):  CED66DE6
addchecksum = address || checkSum:  A0DA40031C5B7895C5C9CEFE211F8D8F0B81CC65D6CED66DE6
base58Address = Base58(addchecksum):  27iyWXqSs8nH6dHngC7TYduFZebvSNsyRk9
-----------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/5'
Private Key: 3FF3B397763DFFD0FEF0C7EBF0C561E9B1C47EF426F67BFC8FE634958192A364
Password = base64(Private Key):  P/Ozl3Y9/9D+8Mfr8MVh6bHEfvQm9nv8j+Y0lYGSo2Q=
Public Key: 0401d0bc19b73127793dd4f61d0faa33d85757d74509a65d71addd87a29cc3cf5ecdd0ac91a6dbb7e7a174f2dc798ebe42e146a200818b496c6af47ed342754db3
sha3 = SHA3(Public Key[1, 65)):  70c60e2a244697fdcc3af7fae0b60285e33aecb8af96b965f6f1a8dd60713769
Address = A0||sha3[12,32): :  A0E0B60285E33AECB8AF96B965F6F1A8DD60713769
sha256_0 = SHA256(Address):  B47A49FF0BFD02CE3A6C0E1BB85F479ED76D4926BEF8BADF3F7B70E3F4CCBDBB
sha256_1 = SHA256(sha256_0):  0870038B8E5A352D225160587072117018B9DABC813697C97096A17F1B4966C1
checkSum = sha256_1[0, 4):  0870038B
addchecksum = address || checkSum:  A0E0B60285E33AECB8AF96B965F6F1A8DD607137690870038B
base58Address = Base58(addchecksum):  27jZfwcQboyqhXYwzUp8mMVMAcaZTroJFz2
-----------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/6'
Private Key: 5A2BC14E1C1593CFFB460644B39CFC843D0CF2818A8F2F6D1BCB6175807EE8E7
Password = base64(Private Key):  WivBThwVk8/7RgZEs5z8hD0M8oGKjy9tG8thdYB+6Oc=
Public Key: 04660a151d8438a7a21086f0d0151b8ef9a5f7d2b3eae9d9a2024c53373dffbae6ab74056cdb6f5e9dc40246eb77400de4573138879362cffbdec6a5d06afd8567
sha3 = SHA3(Public Key[1, 65)):  f8da58e4064f452930371945f864578dc79660e5bbf1ca5ffd439f90e0c3a927
Address = A0||sha3[12,32): :  A0F864578DC79660E5BBF1CA5FFD439F90E0C3A927
sha256_0 = SHA256(Address):  1A119F3237A7E821BCB3495EEF7CD4F6A510175323BB53202788A216A8E479A1
sha256_1 = SHA256(sha256_0):  579C2A7B2D88C5C5C561D4F01DA4ADDF7AAEF17CB998B3D7F2365817791FAE4D
checkSum = sha256_1[0, 4):  579C2A7B
addchecksum = address || checkSum:  A0F864578DC79660E5BBF1CA5FFD439F90E0C3A927579C2A7B
base58Address = Base58(addchecksum):  27mitKqJauSXWUknPZ2EEhSruEWAhNGp1Gn
-----------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/7'
Private Key: F5CE13D16B002ED45CDBDCACE8B9A1293D3A5CF9D590150FF5BDD4E1E03A60BC
Password = base64(Private Key):  9c4T0WsALtRc29ys6LmhKT06XPnVkBUP9b3U4eA6YLw=
Public Key: 04e9e9ee66be746cf850475c8818aebcd2f29f3fd09fc626f9b0a02e8f11a61d5bfa11cf2f6b24ee64d116994bef8a537b51c62d3499cdd0333a82034e1a08fd2f
sha3 = SHA3(Public Key[1, 65)):  7de4025e90017753d22265cae0f9f7c5fcffbfc29bbfe33233ff46ffbd19377b
Address = A0||sha3[12,32): :  A0E0F9F7C5FCFFBFC29BBFE33233FF46FFBD19377B
sha256_0 = SHA256(Address):  0B5360304BD524385EFE0375762192DAF95109065B067B11AA73B46C85C48FF2
sha256_1 = SHA256(sha256_0):  5B55FEEC6A33FBB91D2CC840F0DE990A4B981E6C4610140C70C96FD4E22220AB
checkSum = sha256_1[0, 4):  5B55FEEC
addchecksum = address || checkSum:  A0E0F9F7C5FCFFBFC29BBFE33233FF46FFBD19377B5B55FEEC
base58Address = Base58(addchecksum):  27jb5MR7XKtiHDDQcjJoZpfontKVHUJpW3V
-----------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/8'
Private Key: F3C50D8707881B5350CDEA56B2028414D2C723E3A76D280E21BA53521C2E4E34
Password = base64(Private Key):  88UNhweIG1NQzepWsgKEFNLHI+OnbSgOIbpTUhwuTjQ=
Public Key: 040d2086ec8dbbd007222555f33fb037748ff986f29208049bc77a713653c2ab1acfd67c2856a248d5e6ec8a0300b0bca8ff71b0eba1e44439d52d6d37d4116ed3
sha3 = SHA3(Public Key[1, 65)):  92746dc8e9d6c87fdc6c43eb396c1679404171d2992d139e28e583f120961c84
Address = A0||sha3[12,32): :  A0396C1679404171D2992D139E28E583F120961C84
sha256_0 = SHA256(Address):  D06D1BEB5CEC47D91334E082D729A107609763B61169AF1AA70F4DF53F2174EB
sha256_1 = SHA256(sha256_0):  E337C053DFA56DC73045162BD3ABE7C681FD43E44EF6E29897384BED1BFF03BA
checkSum = sha256_1[0, 4):  E337C053
addchecksum = address || checkSum:  A0396C1679404171D2992D139E28E583F120961C84E337C053
base58Address = Base58(addchecksum):  27UK8YP1XmiQQiVzWkRqesMYL7j6Su9xsgW
-----------------------------------------------------------------
Mnemonic (24 words):  aware present easily example nurse silver ecology plug accident decrease special ceiling federal sketch tackle twenty castle marine miss liquid dutch skate tide acoustic
BIP39 Seed:  469c9422f2ec8a4197d57e2960d9ba578a2326676c0094c09deff347c546d19236148937f7585c843b95cca84498e64e98ef69133f7f7b31cb32be040a5ba22c
BIP39 Path:  m/44'/195'/9'
Private Key: D08623D20AB240159F0E32E28521D7E9FE1A04DFD169A83CA878D58CD1A130E2
Password = base64(Private Key):  0IYj0gqyQBWfDjLihSHX6f4aBN/Raag8qHjVjNGhMOI=
Public Key: 04299b6bcff41af794842832a7125b29d5942b3bf714f580608a37c74cd834eb444f3ff1405bbc8ce3add8a0b5a718fe89792472c3502210c1edfaa182dea32579
sha3 = SHA3(Public Key[1, 65)):  f1ed6be52264df76886e56d2a4124ce6cf4f9791e19b18badd3f512a9f0c7cf4
Address = A0||sha3[12,32): :  A0A4124CE6CF4F9791E19B18BADD3F512A9F0C7CF4
sha256_0 = SHA256(Address):  45FA0167AC9C53406366E63022180BD40388CF66A8C2CC449674426C18A1806F
sha256_1 = SHA256(sha256_0):  6B61FD8D8F65D7A68B5927BCF99BC4A964A014E8E6FDD95B6DAE8FC8D1778ED7
checkSum = sha256_1[0, 4):  6B61FD8D
addchecksum = address || checkSum:  A0A4124CE6CF4F9791E19B18BADD3F512A9F0C7CF46B61FD8D
base58Address = Base58(addchecksum):  27e33HNM6jr5bD7GsHENEAxSafVYmTaPzFW
-----------------------------------------------------------------

```

## Reference
https://github.com/stellar/stellar-protocol/edit/master/ecosystem/sep-0005.md
