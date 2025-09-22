# Ethernaut
(do lần đầu viết nên nhiều chỗ mình giải thích hơi bị dài dòng một chút )
Để bắt đầu làm bài tập thì trước tiên cần cài đặt Metamask.

Học syntax solidity tại đây: https://solidity-by-example.org/. Để chạy thử các lệnh solidity thì mọi người có thể lên Remix IDE: https://remix.ethereum.org
Tiếp theo mình lên trang này để lấy testnet tokens về làm bài: https://cloud.google.com/application/web3/faucet/ethereum/sepolia
![image](https://hackmd.io/_uploads/H1YXPSOigg.png)


## Level 0 - Hello Ethernaut

Bài đầu tiên chủ yếu hướng dẫn mình cách tương tác với instance. 

![image](https://hackmd.io/_uploads/SkfBOSOoeg.png)

Mở console của trình duyệt lên thì nó trông như thế này. Sau đó mình làm theo hướng dẫn ở từng bước của bài. 

Để xem địa chỉ hiện tại của bản thân ta dùng lệnh `player`. 

```
player
'0x658E622E3A07B3A26eE7BcC9b2c0Ab08b06c7C21'
```

Gõ `help()` để xem các utility functions mà Ethernaut cung cấp. 

```javascript
  window.help = function () {
    console.table({
      'player': strings.helperPlayer,
      'ethernaut': strings.helperEthernaut,
      'level': strings.helperLevel,
      'contract': strings.helperContract,
      'instance': strings.helperInstance,
      'version': strings.helperVersion,
      'getBalance(address)': strings.helperGetBalance,
      'getBlockNumber()': strings.helperGetBlockNumber,
      'sendTransaction({options})': strings.helperSendTransaction,
      'getNetworkId()': strings.helperGetNetworkId,
      'toWei(ether)': strings.helperToWei,
      'fromWei(wei)': strings.helperFromWei,
      'deployAllContracts()': strings.helperDeployAllContracts,
    })
  }
}
```

Ở đây `contract` là một object đại diện cho instance mà ta vừa mới spawn. 
Ta sẽ gọi các hàm public thông qua instance này và mỗi lần gọi nó sẽ trả về cho ta một promise vì tương tác với blockchain là tương tác bất đồng bộ. 


![image](https://hackmd.io/_uploads/H1END6usxl.png)

Mọi người có thể xem trước một số hàm như sau. 


Đầu tiên khi gọi `contract.info()` thì nó trả về
```javascript
'You will find what you need in info1().'
```
Ta tiếp tục gọi `info1()`

```javascript
await contract.info1()
'Try info2(), but with "hello" as a parameter.'
```
Gọi `info2()` truyền vào tham số `"hello"`

```javascript
await contract.info2("hello")
'The property infoNum holds the number of the next info method to call.'
```

Như vậy khi gọi `infoNum` nó sẽ trả về số thứ tự của method `info()` tiếp theo mà ta cần gọi 

![image](https://hackmd.io/_uploads/HyDOOT_jxe.png)

```javascript
await contract.info42()
'theMethodName is the name of the next method.'
await contract.theMethodName()
'The method name is method7123949.'
await contract.method7123949()
'If you know the password, submit it to authenticate().'
await contract.password()
'ethernaut0'
await contract.authenticate("ethernaut0")
```
Sau khi xác nhận xong nó sẽ hiện lên yêu cầu giao dịch.

![image](https://hackmd.io/_uploads/HJ0ktTusxx.png)

Nhấn xác nhận và hoàn tất chall. 





![image](https://hackmd.io/_uploads/S1by3ruoxg.png)


## Level 1 -  Fallback

Source code:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Fallback {
    mapping(address => uint256) public contributions;
    address public owner;

    constructor() {
        owner = msg.sender;
        contributions[msg.sender] = 1000 * (1 ether);
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "caller is not the owner");
        _;
    }

    function contribute() public payable {
        require(msg.value < 0.001 ether);
        contributions[msg.sender] += msg.value;
        if (contributions[msg.sender] > contributions[owner]) {
            owner = msg.sender;
        }
    }

    function getContribution() public view returns (uint256) {
        return contributions[msg.sender];
    }

    function withdraw() public onlyOwner {
        payable(owner).transfer(address(this).balance);
    }

    receive() external payable {
        require(msg.value > 0 && contributions[msg.sender] > 0);
        owner = msg.sender;
    }
}
```
Cấu trúc cơ bản của một solidity contract bao gồm: dòng đầu tiên cho ta biết license của contract. Dòng tiếp theo cho ta biết mã nguồn solidity được viết ở phiên bản nào và cuối cùng là phần thân của contract (ở đây ta có mã solidity ở phiên bản 0.8.0)

Ta phân tích từng hàm trong `contract Fallback{}`

```solidity
    mapping(address => uint256) public contributions;
    address public owner;
```
Hàm này map mỗi địa chỉ ví sang các số nguyên 256 bits. Ở đây cũng khai báo một biến địa chỉ của `owner` và được lưu ở state public. Solidity sẽ tự sinh ra một getter function để ai cũng có thể đọc được giá trị  
![image](https://hackmd.io/_uploads/HJCbcJYigl.png)
Trong console nếu gõ như sau thì ta sẽ xem được địa chỉ của owner. 
```solidity
await contract.owner()

'0x3c34A342b2aF5e885FcaA3800dB5B205fEfa3ffB'
```
```solidity
    constructor() {
        owner = msg.sender;
        contributions[msg.sender] = 1000 * (1 ether);
    }
```
Ở đây ta biết được khi contract được deploy thì `owner` sẽ là người deploy và đồng thời ta gán cho `owner` một khoản contributions ban đầu là `1000 ethers`

```solidity
    modifier onlyOwner() {
        require(msg.sender == owner, "caller is not the owner");
        _;
    }
```
Đây là một bộ lọc, chỉ cho phép `owner` gọi hàm.

```solidity
    function contribute() public payable {
        require(msg.value < 0.001 ether);
        contributions[msg.sender] += msg.value;
        if (contributions[msg.sender] > contributions[owner]) {
            owner = msg.sender;
        }
    }
```
Hàm này cho ta biết nhưng thông tin sau: Ta có thể gửi ETH với tối đa là `0.001 ether`. 
Sau đó số lượng này sẽ được cộng thêm vào contributions của owner thông qua `contributions[msg.sender] += msg.value;`

Nếu như giá trị contributions của ta vượt quá 1000 (tức là contributions của owner) thì ta sẽ trở thành owner mới và sẽ được phép gọi hàm. 
```solidity
    function getContribution() public view returns (uint256) {
        return contributions[msg.sender];
    }

```
Hàm này cho biết bản thân đã góp bao nhiêu. 
Và cuối cùng: 
```solidity
    function withdraw() public onlyOwner {
        payable(owner).transfer(address(this).balance);
    }

    receive() external payable {
        require(msg.value > 0 && contributions[msg.sender] > 0);
        owner = msg.sender;
    }
}
```
Hàm `withdraw()` cho phép ta rút toàn bộ số tiền trong ví nếu như ta là `owner`. 

Hàm `receive()` sẽ được gọi khi contract nhận ETH nhưng không có data, đồng thời phải thỏa 2 yêu cầu đó là `msg.value>0` tức là ta phải gửi tiền vào và số tiền trước đó ít nhất phải lớn hơn 0.

Chi tiết hơn thì mình đọc doc ở đây:
![image](https://hackmd.io/_uploads/ry5rlgtsgl.png)

Mình hiểu nó như sau: 
Mỗi contract sẽ có tối đa một hàm `receive`, khai báo bằng cách gọi 
```solidity
receive() external payable {...}
```
Hàm này không có tên, không có tham số và cũng không trả về giá trị gì. 
Hàm này được kích hoạt khi ta call tới contract với data rỗng. 

![image](https://hackmd.io/_uploads/r15y-gKjgl.png)

Tương tự thì ta cũng có một hàm khác gọi là fallback có cú pháp khai báo:
```solidity
fallback() external [payable] { ... }
// hoặc
fallback(bytes calldata input) external [payable] returns (bytes memory output) { ... }
```
Trong trường hợp data rỗng và contract không có `receive()` thì fallback được gọi. Như mọi người thấy thì ở bài này hàm fallback thực chất chính là `receive()`

Mục tiêu của màn này đó là chiếm quyền của owner và rút toàn bộ số dư khỏi tài khoản.
Để làm được thì đầu thì ta cần trở thành contributor bằng cách gọi `contribute()` và gửi một lượng ETH nhỏ hơn 0.001
Nếu gõ `help()` thì mọi người có thể thấy có thể dùng phương thức `toWei` để chuyển tiền. 

```solidity
await contract.contribute({ from: player, value: toWei("0.0001", "ether") });
```
Sau đó gửi ETH tới contract để kích hoạt fallback function
```solidity
await web3.eth.sendTransaction({ from: player, to: contract.address, value: web3.utils.toWei("0.0001", "ether") });
```
Sau đó kiểm tra lại xem ta có phải là owner chưa và rút toàn bộ tiền và submit. 
```solidity
await contract.owner()
contract.withdraw()
```
## Level 2 - Fallout

# Tài liệu
[1] https://ethereum.org/developers/docs/
[2] https://docs.ethers.org/v6/getting-started/