# Intro

Please notice that the method names can be updated in the final release.

=== "Android"

	## Coroutines vs Callback

	This SDK is built with flexibility in mind, offering both modern coroutine support and traditional callbacks for all functions. Whether you prefer the clarity of Kotlin Coroutines or need backward compatibility, you can choose the approach that best fits your project.

	Using coroutines:
    ```kotlin
	launch {
		val result = MobileIdWallet.getInstance().getPassportCredentials()
		
		if (result.isSuccess) {
			val credentials = result.getOrNull()
			// handle success here
		} else {
			// handle error here
		}
	}
    ```

	Using callback:
	```kotlin
	MobileIdWallet.getInstance().getPassportCredentials {
		if (it.isSuccess) {
			val credentials = it.getOrNull()
			// handle success here
		} else {
			// handle error here
		}
	}
	```

=== "iOS"

	## Async/Await vs Completion Handlers

	This SDK is built with flexibility in mind, offering both modern async/await support and traditional completion handlers for all functions. Whether you prefer the clarity of Swift Concurrency or need backward compatibility, you can choose the approach that best fits your project.

	## Async/Await vs Completion Handlers sample

    ```swift
	import MobileIdWalletSDK
	import WalletSDKCore
	
	class ClosureVsAssync {
	    let mobileIdWallet: MobileIdWalletProtocol
	    init(mobileIdWallet: MobileIdWalletProtocol) {
	        self.mobileIdWallet = mobileIdWallet
	    }
	}
	
	extension ClosureVsAssync {
	    func getAllDocumentsAssync() {
	        Task {
	            do {
	                let output = try await mobileIdWallet.getAllDocuments()
	                guard let first = output.records.first else { return }
	                print(first)
	            } catch {
	                print(error)
	            }
	        }
	    }
	
	    func getAllDocumentsCompletionHandler() {
	        mobileIdWallet.getAllDocuments { result in
	            switch result {
	            case .success(let output):
	                guard let first = output.records.first else { return }
	                print(first)
	            case .failure(let error):
	                print(error)
	            }
	        }
	    }
	}
    ```

