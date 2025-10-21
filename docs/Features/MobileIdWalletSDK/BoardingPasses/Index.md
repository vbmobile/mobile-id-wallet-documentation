# Boarding Passes

The Mobile ID Wallet SDK provides robust functionality for managing boarding passes within the wallet. Developers can retrieve all stored boarding passes or access a specific boarding pass by its unique identifier, including full details when needed. Boarding passes can be added to the wallet by parsing images or scanning them directly with the device camera, and they can also be deleted when no longer required. 

All operations are fully asynchronous with async/await support and provide completion handler alternatives for legacy workflows. Inputs and outputs are strongly typed, ensuring safe and predictable access to boarding pass data, while the SDK maintains a consistent Swift-native API style for seamless integration into your app.


## Scan and Parse Boarding Pass

=== "Android"

    ```kotlin
	launch {
        val result = MobileIdWallet.getInstance().scanBoardingPass(
            activity = context,
            input = ScanBoardingPass.Input(BoardingPassParameters(validate = false)),
        )

        if (result.isSuccess) {
            val boardingPass = result.getOrNull()?.records
            // handle success here
        } else {
            // handle error here
        }
    }

    launch {
        val imageUri: Uri = <YOUR_IMAGE_URI>
        val result = MobileIdWallet.getInstance().parseBoardingPass(
            activity = context,
            input = ParseBoardingPass.Input(BoardingPassImageParserParameters(validate = false, uri = imageUri)),
        )

        if (result.isSuccess) {
            val boardingPass = result.getOrNull()?.records
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension BoardingPassManagerSampleUsage {
	    /// Scans a boarding pass using the device camera, parses its information, and stores it in the wallet.
	    func scanBoardingPass() {
	        let viewController = UIViewController()
	        Task {
	            try? await mobileIdWallet.scanBoardingPass(.init(
	                viewController: viewController,
	                parameters: .init(validateBoardingPass: true)
	            ))
	        }
	    }
	
	    /// Parses a boarding pass image to extract flight information and stores it in the wallet.
	    func parseBoardingPass() {
	        let viewController = UIViewController()
	        let boardingPassImage = UIImage()
	        Task {
	            try? await mobileIdWallet.parseBoardingPass(.init(
	                viewController: viewController,
	                parameters: .init(validateBoardingPass: true, boardingPassData: nil, boardingPassImage: boardingPassImage)
	            ))
	        }
	    }
	}
	```
	
## Get all Boarding Passes 

=== "Android"

    ```kotlin
	launch {
        val result = MobileIdWallet.getInstance().getAllBoardingPass()
    
        if (result.isSuccess) {
            val document = result.getOrNull()?.records
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension BoardingPassManagerSampleUsage {
	    /// Retrieves all boarding passes currently stored in the wallet.
	    func getAllBoardingPass() async {
	        Task {
	            let result = try? await mobileIdWallet.getAllBoardingPass()
	            print(result?.records ?? [])
	        }
	    }
	
	    /// Retrieves a specific boarding pass using its unique identifier.
	    func getBoardingPassById() async {
	        let boardingPassId = "your_boarding_pass_id"
	        let result = try? await mobileIdWallet.getBoardingPass(.init(boardingPassId: boardingPassId))
	        guard let boardingPass = result?.record else { return }
	        print(boardingPass)
	    }
	}
	```

## Get a Boarding Pass

=== "Android"

    ```kotlin
	launch {
        val result = MobileIdWallet.getInstance().getBoardingPass(
            input = GetBoardingPass.Input(boardingPassId),
        )
    
        if (result.isSuccess) {
            val boardingPass = result.getOrNull()?.boardingPass
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
    TODO
    ```
	
## Delete

=== "Android"

    ```kotlin
	launch {
        val result = MobileIdWallet.getInstance().deleteBoardingPass(
            input = DeleteBoardingPass.Input(
                boardingPassId = boardingPassId
            )
        )
    
        if (result.isSuccess) {
            // handle success here
        } else {
            // handle error here
        }
    }
    ```

=== "iOS"

    ```swift
	extension BoardingPassManagerSampleUsage {
	    /// Deletes a specific boarding pass using its unique identifier.
	    func deleteBoardingPass() async {
	        let boardingPassId = "your_boarding_pass_id"
	        _ = try? await mobileIdWallet.deleteBoardingPass(.init(boardingPassId: boardingPassId))
	    }
	}
	```
