    function pay(
        address token,
        address payer,
        address recipient,
        uint256 value
    ) internal {
        if (token == WETH9 && address(this).balance >= value) {
            // pay with WETH9
            IWETH9(WETH9).deposit{value: value}(); // wrap only what is needed to pay
            IWETH9(WETH9).transfer(recipient, value);
        } else if (payer == address(this)) {
            // pay with tokens already in the contract (for the exact input multihop case)
            TransferHelper.safeTransfer(token, recipient, value);
        } else {
            // pull payment
            TransferHelper.safeTransferFrom(token, payer, recipient, value);
        }
    }
}

Lack of 0 amount check allows malicious user to create mulltiple 0 payments.

A griefer is able to create as many unuseful payments as they want by simply calling Pay() with value = 0.

Proof of Concept
User calls Pay(0,,,,); 
There is no validation that amount > 0
Function will complete successfully.

###Recommendation###
Add the simple check require(Value > 0, "Amount must be greater than 0");
