# Build Document from DocumentReaderReport

We provide a facade method where the developer can convert a DocumentReaderReport into a Document.

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
	
	class DocumentsManagerSampleUsage {
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

## Build Document from DocumentReaderReport

=== "Android"

    ```kotlin
    launch {
		val result = MobileIdWallet.getInstance().mapDocumentReaderReportToDocument(
            MapDocumentReaderReportToDocument.Input(documentReaderReport)
        )

		if (result.isSuccess && result.getOrNull()?.success == true) {
            val document = result.getOrNull()?.document
			// TODO handle success here
		} else {
			// TODO handle error here
		}
	}
    ```

=== "iOS"

    ```swift
    TODO
    ```

