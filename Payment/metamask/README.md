# Ethereum payments to your site with MetaMask


1. Add HTML Pay Button
		
	```html
	<button class="pay-button">Pay</button>
	```

2. Bind event with add payment button on page load
   ```javascript
	window.addEventListener('load', async () => {
      initPayButton();
  	})
	 ```
3. Check is metamask installed or not. If not installed take to site for download it.
	```javascript
	const initPayButton = () => {
		$('.pay-button').click(async() => {
			if (window.ethereum) {
				//code execute if metamask installed
				//payment code will come here
			}else{
				// change google.com to your domain 
				// below code take to website for downloading metamask extension or mobile app.
				window.open('https://metamask.app.link/dapp/google.com/dashboard?login=metamask');
			}
		});
	}
	```

4. It will try get conntec metamask with your site as permission.
	```javascript
		if (window.ethereum) {
			try{
			 //take permission to connect with metamask
			 await ethereum.enable();
	    }catch(e){
				//if not able get access it will come in this block with error message
				$('#status').html('User denied account access', err)
			}			 

		}
	```

5. Now below code will try to make transaction for collecting payment from metamask.
   ```javascript
	 	await ethereum.enable();
		// paymentAddress is where funds will be send to
		const paymentAddress = '0xF62b9Cxxxxxxxxxxxx'
		const amountEth = 1; // amount which you want to charge
		web3.eth.sendTransaction({
			to: paymentAddress,
			value: web3.toWei(amountEth, 'ether') //it will convert amount in wei
			}, (err, transactionId) => {
			if  (err) {
				//on payment success
				console.log('Payment failed', err)
				$('#status').html('Payment failed')
			} else {
					//on payment fail
				console.log('Payment successful', transactionId)
				$('#status').html('Payment successful')
			}
		})
	 ```