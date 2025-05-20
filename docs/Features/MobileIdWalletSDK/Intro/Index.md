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
	
	    func getPassportCredentialsAssync() {
	        Task {
	            do {
	                let output = try await mobileIdWallet.getPassportCredentials(.init())
	                guard let verifiedIdEntity = output.records.first else { return }
	                print(verifiedIdEntity)
	            } catch {
	                print(error)
	            }
	        }
	    }
		
	    func getPassportCredentialsCompletionHandler() {
	        mobileIdWallet.getPassportCredentials(.init()) { result in
	            switch result {
	            case .success(let output):
	                guard let verifiedIdEntity = output.records.first else { return }
	                print(verifiedIdEntity)
	            case .failure(let error):
	                print(error)
	            }
	        }
	    }
	}
    ```

