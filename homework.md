# Hello World

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract HelloWorld {
    string public greet = 'Hello World!';
}
```

# First App

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract FirstApp {
    uint256 count;

    function getCount() public view returns (uint256) {
        return count;
    }

    function incCount() public {
        count += 1;
    }

    function decCount() public {
        require(count > 0, "Count cannot be negative");
        count -= 1;
    }
}

```

# Primitive Data Types

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract Primitives {
    bool public boo = true;

    /*
    uint stands for unsigned integer, meaning non negative integers
    different sizes are available
        uint8   ranges from 0 to 2 ** 8 - 1
        uint16  ranges from 0 to 2 ** 16 - 1
        ...
        uint256 ranges from 0 to 2 ** 256 - 1
    */
    uint8 public u8 = 1;
    uint256 public u256 = 456;
    uint256 public u = 123;

    /*
    Negative numbers are allowed for int types.
    Like uint, different ranges are available from int8 to int256
    
    int256 ranges from -2 ** 255 to 2 ** 255 - 1
    int128 ranges from -2 ** 127 to 2 ** 127 - 1
    */
    int8 public i8 = -1;
    int256 public i256 = 256;
    int256 public i = -123;

    // minimum and maximum of int
    int256 public minInt = type(int256).min;
    int256 public maxInt = type(int256).max;

    address public addr = 0xCA35b7d915458EF540aDe6068dFe2F44E8fa733c;

    /*
    In Solidity, the data type byte represent a sequence of bytes. 
    Solidity presents two type of bytes types :

     - fixed-sized byte arrays
     - dynamically-sized byte arrays.
     
     The term bytes in Solidity represents a dynamic array of bytes. 
     It’s a shorthand for byte[] .
    */
    bytes1 a = 0xb5;
    bytes1 b = 0x56;

    // Default values
    // Unassigned variables have a default value
    bool public defaultBoo; // false
    uint256 public defaultUint; // 0
    int256 public defaultInt; // 0
    address public defaultAddr; // 0x0000000000000000000000000000000000000000
}
```

# Variables

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract Variables {
    // State variables are stored on the blockchain.
    string public str = 'storedVariables';
    uint public num = 123;

    function doSomething() public view {
        // Local variables are not saved to the blockchain.
        uint256 i = 456;

        // Here are some global variables
        uint256 timestamp = block.timestamp;
        address sender = msg.sender;
    }
}
```

# Constants

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract Constants {
    // coding convention to uppercase constant variables
    address public constant MY_ADDRESS = 0x777788889999AaAAbBbbCcccddDdeeeEfFFfCcCc;
    uint256 public constant MY_UINT = 123;
}
```

# Immutable

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract Immutable {
    // Immutable variables are like constants. Values of immutable variables can be set inside the constructor but cannot be modified afterwards.
    address public immutable MY_ADDRESS;
    uint256 public immutable MY_UINT;

    constructor (uint256 _myUint) {
        MY_ADDRESS = msg.sender;
        MY_UINT = _myUint;
    }
}
```

# Reading and Writing to a State Variable

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract SimpleStorage  {
    uint public num;

    function setNum(uint _num) public {
        num = _num;
    }

    function getNum() public view returns (uint) {
        return num;
    }
}
```

# Ether and Wei

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract EtherUnits  {
    uint public oneWei = 1 wei;
    bool isOnewei = (oneWei == 1);

    uint public oneGwei = 1 gwei;
    bool public isOneGwei = (oneGwei == 1e9);

    uint public oneEther = 1 ether;
    bool public isOneEther = (oneEther == 1e18);
}
```

# Gas Limit

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract Gas  {
    // Using up all of the gas that you send causes your transaction to fail.
    // State changes are undone.
    // Gas spent are not refunded.
    uint i = 0;
    function forever() public {
        while (true) {
            i += 1;
        }
    }
}
```

# If / Else

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract IfElse {
    function foo(uint256 x) public pure returns (uint256) {
        if (x < 10) {
            return 0;
        } else if (x < 20) {
            return 1;
        } else {
            return 2;
        }
    }

    function ternary(uint256 _x) public pure returns (uint256) {
        // if (_x < 10) {
        //     return 1;
        // }
        // return 2;

        // shorthand way to write if / else statement
        // the "?" operator is called the ternary operator
        return _x < 10 ? 1 : 2;
    }
}
```

# For and While Loop

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Loop {
    function loop() public {
        // for loop
        for (uint256 i = 0; i < 10; i++) {
            if (i == 3) {
                // Skip to next iteration with continue
                continue;
            }
            if (i == 5) {
                // Exit loop with break
                break;
            }
        }

        // while loop
        uint256 j;
        while (j < 10) {
            j++;
        }
    }
}
```

# Mapping

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract Mapping {
    mapping(address => uint256) public myMap;

    function get(address _addr) public view returns (uint256) {
        return myMap[_addr];
    }

    function set(address _addr, uint256 _i) public {
        myMap[_addr] = _i;
    }

    function rmove(address _addr) public {
        delete myMap[_addr];
    }
}

contract NestedMapping {
    mapping(address => mapping(uint256 => bool)) public nested;

    function get(address _addr, uint256 _i) public view returns (bool) {
        return nested[_addr][_i];
    }

    function set(address _addr, uint256 _i, bool _boo) public {
        nested[_addr][_i] = _boo;
    }

    function rmove(address _addr, uint256 _i) public {
        delete nested[_addr][_i];
    }
}
```

# Array

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Array {
    // Several ways to initialize an array
    uint256[] public arr;
    uint256[] public arr2 = [1, 2, 3];
    // Fixed sized array, all elements initialize to 0
    uint256[10] public myFixedSizeArr;

    function get(uint256 i) public view returns (uint256) {
        return arr[i];
    }

    // Solidity can return the entire array.
    // But this function should be avoided for
    // arrays that can grow indefinitely in length.
    function getArr() public view returns (uint256[] memory) {
        return arr;
    }

    function push(uint256 i) public {
        // Append to array
        // This will increase the array length by 1.
        arr.push(i);
    }

    function pop() public {
        // Remove last element from array
        // This will decrease the array length by 1
        arr.pop();
    }

    function getLength() public view returns (uint256) {
        return arr.length;
    }

    function remove(uint256 index) public {
        // Delete does not change the array length.
        // It resets the value at index to it's default value,
        // in this case 0
        delete arr[index];
    }

    function examples() external {
        // create array in memory, only fixed size can be created
        uint256[] memory a = new uint256[](5);
    }
}
```

# Examples of removing array element

```solidity

```
