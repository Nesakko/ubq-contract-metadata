# Ubiq Contract Metadata

A mapping of checksummed ubiq addresses to metadata, like names, and images of those addresses' logos.

All address keys follow the [EIP 55 address checksum format](https://github.com/ethereum/EIPs/issues/55).

## Usage

You can install from npm with `npm install ubq-contract-metadata` and use it in your code like this:

```javascript
import contractMap from 'ubq-contract-metadata'
import ethJSUtil from 'ethereumjs-util'
const { toChecksumAddress } = ethJSUtil

function imageElFor (address) {
  const metadata = contractMap[toChecksumAddress(address)]
  if (metadata?.logo) {
    const fileName = metadata.logo
    const path = `${__dirname}/images/contract/${fileName}`
    const img = document.createElement('img')
    img.src = path
    img.style.width = '100%'
    return img
  }
}

imageElFor ("0x06012c8cf97BEaD5deAe237070F9587f8E7A266d")
```

## Submission Process

Maintaining this list is a considerable chore, and it is not our highest priority. We do not guarantee inclusion in this list on any urgent timeline. We are actively looking for fair and safe ways to maintain a list like this in a decentralized way, because maintaining it is a large and security-delicate task.

1. Fork this repository.
2. Add your logo image to the `images` folder. PNG or SVG format, square, transparent background, maximum pixel size of 256x256 and maximum file size of 100kB.
3. Add an entry to the `contract-map.json` file with the specified address as the key, and the image file's name as the value.

Criteria:

- Do not add your entry to the end of the JSON map, messing with the trailing comma. Your pull request should only be an addition of lines, and any line removals should be deliberate deprecations of those logos.
- PR should include link to official project website referencing the suggested address.
- Project website should include explanation of project.
- Project should have clear signs of activity, either traffic on the network, activity on GitHub, or community buzz.
- Nice to have a verified source code on [Sourcify](https://sourcify.dev).

A sample submission:

```json
{
  "0x6090A6e47849629b7245Dfa1Ca21D94cd15878Ef": {
    "name": "ENS Registrar",
    "logo": "ens.svg"
  }
}
```

Tokens should include a field `"erc20": true`, and can include additional fields:

- symbol (a five-character or less ticker symbol)
- decimals (precision of the tokens stored)

A full list of permitted fields can be found in the [permitted-fields.json](./permitted-fields.json) file.
