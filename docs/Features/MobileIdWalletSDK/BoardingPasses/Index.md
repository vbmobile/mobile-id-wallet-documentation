# Boarding Passes

The Mobile ID Wallet SDK provides robust functionality for managing boarding passes within the wallet. Developers can retrieve all stored boarding passes or access a specific boarding pass by its unique identifier, including full details when needed. Boarding passes can be added to the wallet by parsing images or scanning them directly with the device camera, and they can also be deleted when no longer required. 

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
    func scanBoardingPass() {
        let viewController = UIViewController()
        Task {
            do {
                let output = try await mobileIdWallet.scanBoardingPass(.init(
                    viewController: viewController,
                    parameters: .init(validateBoardingPass: true)
                ))
                let boardingPass = output.boardingPass
                // handle success here
            } catch {
                // handle error here
            }
        }
    }
	
    func parseBoardingPass() {
        let viewController = UIViewController()
        let boardingPassImage = UIImage()
        Task {
            do {
                let output = try await mobileIdWallet.parseBoardingPass(.init(
                    viewController: viewController,
                    parameters: .init(validateBoardingPass: true, boardingPassData: nil, boardingPassImage: boardingPassImage)
                ))
                let boardingPass = output.boardingPass
                // handle success here
            } catch {
                // handle error here
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
    Task {
        do {
            let output = try await mobileIdWallet.getAllBoardingPass()
            let records = output.records
            // handle success here
        } catch {
            // handle error here
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
    Task {
        do {
            let boardingPassId = "<YOUR_BOARDING_PASS_ID>"
            let output = try await mobileIdWallet.getBoardingPass(.init(boardingPassId: boardingPassId))
            let boardingPass = output.record
            // handle success here
        } catch {
            // handle error here
        }
    }
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
    Task {
        do {
            let boardingPassId = "<YOUR_BOARDING_PASS_ID>"
            let output = try await mobileIdWallet.deleteBoardingPass(.init(boardingPassId: boardingPassId))
            if (output.success) {
                // handle success here
            } else {
                // handle error here
            }
        } catch {
            // handle error here
        }
    }
	```
