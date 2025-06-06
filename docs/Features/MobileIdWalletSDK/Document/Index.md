# Build Document Data from DocumentReaderReport

We provide a facade method where the developer can convert a DocumentReaderReport into a Document.

## Build Document data

=== "Android"

    ```kotlin
    launch {
		val result = MobileIdWallet.getInstance().buildDocumentData(
            MapDocumentReaderReportToDocumentData.Input(documentReaderReport)
        )

		if (result.isSuccess && result.getOrNull()?.success == true) {
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

