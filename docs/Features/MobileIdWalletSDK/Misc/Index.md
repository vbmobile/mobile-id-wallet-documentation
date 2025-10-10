# Misc Operations

The Mobile ID Wallet SDK provides additional utility functions to simplify wallet management. This includes operations such as batch deleting multiple documents or boarding passes at once, allowing developers to efficiently manage wallet contents. These miscellaneous functions complement the main workflows for document and boarding pass handling, providing flexibility and control over stored data.

All operations support Swift’s async/await concurrency model, with optional completion handler alternatives for callback-based workflows. Strongly typed inputs and outputs ensure safe, predictable access to data, and the API maintains a consistent Swift-native style for seamless integration into your app.


## Setup

=== "Android"

    ```kotlin
	val walletSdkConfig = WalletSdkConfig(
        ...
    ) 
    MobileIdWallet.initialize(
        context = this,
        walletConfig = walletSdkConfig,
        onEnrolmentInitialized = { success, error ->
            if (!success) {
                print(error)
            }
        }
    )
    ```

=== "iOS"

    ```swift
	import Foundation
	import WalletSDKCore
	import MobileIdWalletSDK
	import MobileIdSDKiOS // MobileID (VB Enrollment SDK)
	
	class MiscSampleUsage {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	
	    init(input: MobileIdWalletSetup.Input) {
	        self.mobileIdWallet = MobileIdWallet.shared
	        mobileIdWallet.setup(.init(mobileIdWalletConfig: input.mobileIdWalletConfig))
	    }
	}
	```
	
## Batch Delete

=== "Android"

    ```kotlin
	launch {
        val result = MobileIdWallet.getInstance().batchDelete()

        if (result.isSuccess) {
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension MiscSampleUsage {
	    /// Deletes all content from the wallet.
	    func batchDelete() {
	        Task {
	            await mobileIdWallet.batchDelete()
	        }
	    }
	}
	```

