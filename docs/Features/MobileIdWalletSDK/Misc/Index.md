# Misc Operations

The Mobile ID Wallet SDK provides additional utility functions to simplify wallet management. This includes operations such as batch deleting multiple documents or boarding passes at once, allowing developers to efficiently manage wallet contents. These miscellaneous functions complement the main workflows for document and boarding pass handling, providing flexibility and control over stored data.
	
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
	        mobileIdWallet.batchDelete()
	    }
	}
	```

