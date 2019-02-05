# BchJS: Bitcoin Cash library blockchain interaction and different purpose for Node.js and web browsers.


Easy JavaScript library for Bitcoin Cash blockchain interaction needs. Easy-to-use, thoroughly tested and complete.

Support for the new Bitcoin Cash address ABC which improves upon [BIP 173](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki), as well as the Bitpay and Legacy formats.

Test a demo address translator powered by BchAddr.js [here](https://bitcoincashjs.github.io/address/).

## Installation

### Web Browser Manually Script Tag

You may include a script tag in your HTML and the `bchaddr` module will be defined globally on subsequent scripts.

```html
<html>
  <head>
    ...
    <script src="https://github.com/rafaelosiris/bchjs/library/bchaddrjs-0.3.0.min.js"></script>
  </head>
  ...
</html>
```

## Code Examples

### Supported formats, networks and address types.
```javascript
var Format = bchaddr.Format; // Legacy, Bitpay or Cashaddr.
var Network = bchaddr.Network; // Mainnet or Testnet.
var Type = bchaddr.Type; // P2PKH or P2SH.
```


```HTML
<html>
	<head>
		<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>	
		<script src="https://cdn.jsdelivr.net/gh/rafaelosiris/bchjs/library/bchaddrjs-0.3.0.min.js"></script>
		<script src="https://cdn.jsdelivr.net/gh/rafaelosiris/bchjs/library/bitcoincashjs.0.1.7.min.js"></script>
	
	</head>
	
	<body>
	
	


<!-- BEGIN PAGE CONTAINER-->
<div class="page-content"> 
  <div class="clearfix"></div>
	  <div class="content">    
		  <div class="page-title" style="display:"> <a href="#" id="btn-back"><i class="icon-custom-left"></i></a>
			  <h3>BCHJS LIBRARY - <span class="semi-bold"> VIEW ON  <a href="https://github.com/rafaelosiris/bchjs">GITHUB</a> </span></h3>
		   </div>	
		  <hr>
		  <h3>BCHJS BLOCKCHAIN FUNCTIONS</h3>
		  <hr>					
		  <div class="row-fluid">
				  <div class="span12">
				  Create Wallet: <button id="cWallet" class="button">create wallet</button>
				  <br />
				  </div>
		  </div>
		  <div id="msg"></div>
		  
		  <hr>					
		  <div class="row-fluid">
				  <div class="span12">
				  Verify Wallet: <input type="text" id="vText" /> <button id="vWallet" class="button">verify wallet</button>
				  <br />
				  </div>
		  </div>
		  <div id="vmsg"></div>	
		  
		  
		  <hr>					
		  <div class="row-fluid">
				  <div class="span12">
				  Balance of Account: <br />
				  <input type="text" id="bText" placeholder="PUT THE PUBLIC KEY HERE" size="50" /> <br />
				  
				  <button id="bWallet" class="button">verify Balance</button>
				  <br />
				  GET FREE BCH FAUCET TO TEST <a href="https://developer.bitcoin.com/faucets/bch/" target=_blank>HERE</a>
				  <br /><br />
				  </div>
		  </div>
		  <div id="bmsg"></div>			  
		  
		  <hr>					
		  <div class="row-fluid">
				  <div class="span12">
				  Transfer BCH: <br />
				  <input type="text" id="pfTx" placeholder="PUT THE SENDER PRIVATE KEY HERE" size="50" /><br />
				  <input type="text" id="ptTx" placeholder="PUT THE RECEIVER PUBLIC KEY HERE" size="50" /> <br />
				  <input type="number" id="aTx" placeholder="AMOUNT TO TRANSFER" /> <br />
				  
				  <button id="tWallet" class="button">Transfer</button>
				  <br />
				  </div>
		  </div>
		  <div id="tmsg"></div>			  


   </div>
</div>  
	
	
	
	</body>
	
	  <script>
		  $(document).ready(function()
		  {	
		  /* JAVASCRIPT CREATE WALLET BITCOIN CASH FUNCTIONS */
			var Format = bchaddr.Format; // Legacy, Bitpay or Cashaddr.
			var Network = bchaddr.Network; // Mainnet or Testnet.
			var Type = bchaddr.Type; // P2PKH or P2SH.

			var isLegacyAddress = bchaddr.isLegacyAddress;
			var isBitpayAddress = bchaddr.isBitpayAddress;
			var isCashAddress = bchaddr.isCashAddress;	
			var toCashAddress = bchaddr.toCashAddress;
			
			
			//create wallet
			 $('#cWallet').click(function() {
				const privateKey = bch.PrivateKey('testnet'); 
				
				//const address = privateKey.toAddress();  //livenet
				const address = privateKey.toAddress('testnet');  //testnet

				var exported = privateKey.toWIF();
				var pkey = exported.toString();
				var legacyaddress = address.toString();
				var cashaddress = toCashAddress(address.toString());
				var msg = 'Private Key: *'+pkey+'* <br /> Public CASH Key: *'+cashaddress+'* <br /> Public Legacy Key: *'+legacyaddress+'*';
				$('#msg').html( msg );
			});
			
			//verify wallet
			 $('#vWallet').click(function() {
			 
				var vInput = $('#vText').val();				
				const wif2 = vInput;
				//const wif2 = 'L16d3gWfjTndJEfMcd8hSWwkFcUcZt5r1HhLhrLUtbDQC6hzQYQv';
				var imported2 = bch.PrivateKey.fromWIF(wif2);
				const address2 = imported2.toAddress(); 				
				var detectAddressNetwork = bchaddr.detectAddressNetwork;				
				var msg = 'Legacy Address: '+address2.toString()+ '<br /> Network: '+detectAddressNetwork(address2.toString());
				$('#vmsg').html( '' );
				$('#vmsg').html( msg );
			});	
			
			//balance amount
			 $('#bWallet').click(function() {
			 
				var vInput = $('#bText').val();				
			

				
				
				//Get the balance by restfull bitcoin.com --- this rest is in the test net, for mainnet just change trest for rest.
					 $.ajax({
						 url: "https://trest.bitcoin.com/v1/address/details/"+vInput+""
						}).then(function(data2)
						{ 
						 console.log("Data2 Length: "+data2.length);

							var msg = 'BALANCE: '+data2.balance+'<br /> BALANCE SATOSHI: '+data2.balanceSat+'<br /> <b>UNCONFIRMED TXS</b> </br> Transactions: '+data2.unconfirmedTxApperances+' <br /> Unconfirmed Balance: '+data2.unconfirmedBalance;
							$('#bmsg').html( '' );
							$('#bmsg').html( msg );							
						});				
				
				

			});				
			
			
			//transfer amount
			 $('#tWallet').click(function() {
			 
				var vInput = $('#vText').val();				
				const wif2 = vInput;
				//const wif2 = 'L16d3gWfjTndJEfMcd8hSWwkFcUcZt5r1HhLhrLUtbDQC6hzQYQv';
				var imported2 = bch.PrivateKey.fromWIF(wif2);
				const address2 = imported2.toAddress(); 				
				var detectAddressNetwork = bchaddr.detectAddressNetwork;				
				var msg = 'Legacy Address: '+address2.toString()+ '<br /> Network: '+detectAddressNetwork(address2.toString());
				$('#vmsg').html( '' );
				$('#vmsg').html( msg );
			});				
			
			
		  });	
		 /* END */
		 </script> 	

</html>
```
 

## Documentation and Help

rafaelosiris@gmail.com 

