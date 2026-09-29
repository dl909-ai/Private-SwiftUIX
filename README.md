 SwiftUIX

SwiftUIX aims to fill gaps in SwiftUI by providing an extensive suite of components, extensions, and utilities that complement Apple’s standard library. The project provides a broad collection of SwiftUI-compatible ports and utilities for UIKit and AppKit functionality.

* Why
* Requirements
* Installation
* Documentation
* Contents
* Contributing
* License
* Support
* Credits

Why

The goal of SwiftUIX is to complement SwiftUI by providing additional views, components, extensions, and utilities that make it easier to build applications across Apple’s platforms.

Requirements

[!NOTE]
Swift 5.10 is the minimum Swift version required to build SwiftUIX. Swift 5.9 is no longer supported.

* Deployment targets:
    * iOS 13
    * macOS 11
    * Mac Catalyst 13
    * tvOS 13
    * watchOS 6
    * visionOS 1
* Minimum Xcode version: Xcode 15.4+
* CI configuration includes Xcode 16.x and Xcode 26.x
* CI configuration includes destinations for:
    * iOS
    * macOS
    * Mac Catalyst
    * tvOS
    * watchOS
    * visionOS

The presence of a CI configuration does not by itself establish that a workflow was executed or that a particular build succeeded. CI execution and results are established by the corresponding GitHub Actions run records.

Installation

The preferred installation method is Swift Package Manager.

// Package.swift
dependencies: [
    .package(
        url: "https://github.com/SwiftUIX/SwiftUIX.git",
        branch: "master"
    ),
]

Xcode provides integrated Swift Package Manager support for Apple platforms.

Add SwiftUIX through Xcode

1. Open your project in Xcode.
2. Select File → Add Package Dependencies…
3. Enter:
    https://github.com/SwiftUIX/SwiftUIX
4. Select the desired package version or branch.
5. Add the SwiftUIX product to your target.

Documentation

SwiftUIX documentation is available at:

https://swiftuix.github.io/SwiftUIX/documentation/swiftuix/

Documentation that has not yet been migrated to DocC may be available through the repository wiki.

The existence of documentation source files or a documentation URL does not by itself establish a particular documentation deployment workflow or deployment execution.

Contents

SwiftUIX provides a collection of components, extensions, and utilities intended to complement SwiftUI.

UIKit → SwiftUI

UIKit	SwiftUI	SwiftUIX
LPLinkView	-	LinkPresentationView
UIActivityIndicatorView	-	ActivityIndicator
UIActivityViewController	-	AppActivityView
UIBlurEffect	-	BlurEffectView
UICollectionView	-	CollectionView
UIDeviceOrientation	-	DeviceLayoutOrientation
UIImagePickerController	-	ImagePicker
UIPageViewController	-	PaginationView
UIScreen	-	Screen
UISearchBar	-	SearchBar
UIScrollView	ScrollView	CocoaScrollView
UISwipeGestureRecognizer	-	SwipeGestureOverlay
UITableView	List	CocoaList
UITextField	TextField	CocoaTextField
UIModalPresentationStyle	-	ModalPresentationStyle
UIViewControllerTransitioningDelegate	-	UIHostingControllerTransitioningDelegate
UIVisualEffectView	-	VisualEffectView
UIWindow	-	WindowOverlay

Activity

ActivityIndicator

ActivityIndicator()
    .animated(true)
    .style(.large)

AppActivityView

A SwiftUI interface for UIActivityViewController.

AppActivityView(activityItems: [...])
    .excludeActivityTypes([...])
    .onCancel { }
    .onComplete { result in
        foo(result)
    }

Appearance

* View/visible(_:) - Controls a view’s visibility.

CollectionView

Use CollectionView within a SwiftUI view by providing a data source and a cell-building closure.

import SwiftUIX
struct MyCollectionView: View {
    let data: [MyModel]
    var body: some View {
        CollectionView(data, id: \.self) { item in
            Text(item.title)
        }
    }
}

Error Handling

* TryButton - A button capable of performing throwing functions.

Geometry

* flip3D(_:axis:reverse:) - Flips a view in three-dimensional space.
* RectangleCorner - Represents a corner of a rectangle.
* ZeroSizeView - Provides a zero-sized view where EmptyView is insufficient.

Keyboard

* Keyboard - Represents keyboard-related state.
* View/padding(.keyboard) - Adds padding corresponding to the active keyboard height.

Link Presentation

Use LinkPresentationView to display a link preview for a URL.

LinkPresentationView(url: url)
    .frame(height: 192)

Navigation Bar

* View/navigationBarColor(_:) - Configures the navigation bar color.
* View/navigationBarTranslucent(_:) - Configures navigation bar translucency.
* View/navigationBarTransparent(_:) - Configures navigation bar transparency.
* View/navigationBarLargeTitle(_:) - Configures a custom view for the navigation bar’s large-title mode.

Pagination

PaginationView

PaginationView(axis: .horizontal) {
    ForEach(0..<10, id: \.hashValue) { index in
        Text(String(index))
    }
}
.currentPageIndex($...)
.pageIndicatorAlignment(...)
.pageIndicatorTintColor(...)
.currentPageIndicatorTintColor(...)

Scrolling

View/isScrollEnabled(_:) controls whether supported SwiftUIX scrolling views can be scrolled.

Supported SwiftUIX views include:

* CocoaList
* CocoaScrollView
* CollectionView
* TextView

This modifier does not apply to SwiftUI’s native ScrollView.

Search

SearchBar

A SwiftUI interface for UISearchBar.

struct ContentView: View {
    @State private var isEditing = false
    @State private var searchText = ""
    var body: some View {
        SearchBar(
            "Search...",
            text: $searchText,
            isEditing: $isEditing
        )
        .showsCancelButton(isEditing)
        .onCancel {
            print("Canceled!")
        }
    }
}

View/navigationSearchBar(_:)

Adds a search bar to the navigation interface.

Text("Hello, world!")
    .navigationSearchBar {
        SearchBar("Placeholder", text: $text)
    }

View/navigationSearchBarHiddenWhenScrolling(_:)

Controls whether the integrated search bar is hidden while scrolling underlying content.

Screen

* Screen - Represents the device screen.
* UserInterfaceIdiom - A SwiftUI-compatible representation of UIUserInterfaceIdiom.
* UserInterfaceOrientation - A SwiftUI-compatible representation of UIInterfaceOrientation.

Scroll

* ScrollIndicatorStyle - Describes the appearance and interaction of scroll indicators within a view hierarchy.
* HiddenScrollViewIndicatorStyle - A scroll indicator style that hides scroll indicators within a view hierarchy.

Status Bar

View/statusItem(id:image:)

Adds a status bar item that presents a popover when selected.

Text("Hello, world!")
    .statusItem(id: "foo", image: .system(.exclamationmark)) {
        Text("Popover!")
            .padding()
    }

Text

TextView

TextView(
    "placeholder text",
    text: $text,
    onEditingChanged: { editing in
        print(editing)
    }
)

Visual Effects

VisualEffectBlurView

VisualEffectBlurView(blurStyle: .dark)
    .edgesIgnoringSafeArea(.all)

Window

View/windowOverlay(isKeyAndVisible:content:)

Makes a window key and visible while the supplied condition is true.

Edit Menu

View/editMenu(isVisible:content:)

Adds an edit menu to a view.

Text("Hello, world!")
    .editMenu(isVisible: $isEditMenuVisible) {
        EditMenuItem("Copy") {
            // Perform copy action
        }
        EditMenuItem("Paste") {
            // Perform paste action
        }
    }

Contributing

SwiftUIX welcomes contributions through GitHub issues and pull requests.

Before opening an issue or requesting a feature, check the projects section for related work.

SwiftUIX is a Swift package. To work on the project in Xcode, open Package.swift from the cloned repository.

To perform a local macOS build, run:

xcodebuild \
    -scheme SwiftUIX \
    -destination 'generic/platform=macOS' \
    build

A local build command documents a verification procedure. Successful execution must be established by the corresponding build output.

License

SwiftUIX is licensed under the MIT License.

Support

SwiftUIX is free and open source.

Maintaining SwiftUIX requires substantial ongoing effort. If SwiftUIX is useful to your application or project, you can support the project by:

* Contributing
* Donating via Patreon

Credits

SwiftUIX is led and maintained by @vatsal_manot.

Special thanks to Brett Best, Nathan Tanner, Kabir Oberai, and the many other contributors to the project.