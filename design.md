Design
==

Classes
--

```java
// UI specific
// Categories to organize the downloads conveniently
class DownloadCategory
	String name
	String targetDirectory
	boolean canSetTargetDir = true
	List<DownloadCategory> childs
	void addChild(DownloadCategory childCategory)
		// sets canSetTargetDir to false

// Queues to schedule/queue downloads instead of concurrent downloads
class DownloadQueue
	String name
	// Will help in organizing the directories
	Category category
	LocalTime startsAt
	LocalTime stopsAt
	int maxActiveDownloads

class Settings
	boolean autoTakeOverDownloadsWithKnownExtension
	// Where to save the data
	List<String> knowsExtensions
	// Runtime affects
	int numberOfMaxConnections
	int bufferSize
	Map<String, DownloadQueue> queueAliasToQueue
	Map<String, Credential> authenticationAliasToCredential
	Credential proxyServerCredential

class Credential
	String host
	String port
	String username
	String password

class DownloadCommand
	private DownloadCommand()
	class Builder
		name()
		path()
		url()
		immediate()
		addToQueue()
		username()
		password()
		NewDownloadCommand build()
	String immediate
	String url
	// Authentication info. We only support BASIC authentication
	String username
	String password
	boolean immediate
	// Queue related info
	boolean queued = false
	String queueName
	void setQueueName(String queueName)
		// sets queued flag

interface Handler
	boolean supportsProtocol()
	void handle(DownloadCommand downloadCommand)

class HttpHandler -> Handler
	boolean supports()

class DownloadChunk
	int startIndex
	int lastKnownIndex
	int plannedEndIndex

class DownloadInfo
	String path
	String size
	List<DownloadChunk> chunks
	boolean areAllChunksAvailableLocally()
	boolean didAssembleComplete()
	boolean isDownloadComplete()
```	

> Written with [StackEdit](https://stackedit.io/).