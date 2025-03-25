
Swift Style Guide
=================

![Swift](https://img.shields.io/badge/Swift-4.2-orange.svg)
[![Creative Commons License](https://img.shields.io/badge/license-CC--BY--4.0-blue.svg)](http://creativecommons.org/licenses/by/4.0/)

StyleShare thành viên xây dựng hướng dẫn phong cách giúp mã Swift dễ hiểu và rõ ràng. Các quyết định có thể thay đổi thường xuyên tùy theo sự đồng thuận của các thành viên.

Các quy tắc không có trong tài liệu này sẽ theo các tài liệu dưới đây.

- [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines)
- [SE-0005](https://github.com/apple/swift-evolution/blob/master/proposals/0005-objective-c-name-translation.md)

## Mục lục

- [Cấu trúc mã](#cấu-trúc-mã)
  - [Thụt lề và khoảng trắng](#thụt-lề-và-khoảng-trắng)
  - [Chuyển dòng](#chuyển-dòng)
  - [Chiều dài dòng tối đa](#chiều-dài-dòng-tối-đa)
  - [Dòng trống](#dòng-trống)
  - [Nhập khẩu](#nhập-khẩu)
- [Đặt tên](#đặt-tên)
  - [Lớp và cấu trúc](#lớp-và-cấu-trúc)
  - [Hàm](#hàm)
  - [Biến](#biến)
  - [Hằng số](#hằng-số)
  - [Liệt kê](#liệt-kê)
  - [Giao thức](#giao-thức)
  - [Viết tắt](#viết-tắt)
  - [Delegate](#delegate)
- [Closures](#closures)
- [Lớp và cấu trúc](#lớp-và-cấu-trúc)
- [Kiểu](#kiểu)
- [Chú thích](#chú-thích)
- [Khuyến nghị lập trình](#khuyến-nghị-lập-trình)

## Cấu trúc mã

### Thụt lề và khoảng trắng

- Sử dụng 2 khoảng trắng thay vì tab cho thụt lề.
- Đặt một khoảng trắng sau dấu hai chấm (`:`).

    ```swift
    let names: [String: String]?
    ```

- Trong định nghĩa hàm overload toán tử, để một khoảng trắng giữa toán tử và dấu ngoặc.

    ```swift
    func ** (lhs: Int, rhs: Int)
    ```

### Chuyển dòng

- Nếu định nghĩa hàm vượt quá độ dài tối đa, hãy chuyển dòng như sau:

    ```swift
    func collectionView(
      _ collectionView: UICollectionView,
      cellForItemAt indexPath: IndexPath
    ) -> UICollectionViewCell {
      // doSomething()
    }
    ```

- Nếu mã gọi hàm vượt quá độ dài tối đa, chuyển dòng dựa trên tên tham số.

    ```swift
    let actionSheet = UIActionSheet(
      title: "Bạn có thật sự muốn xóa tài khoản không?",
      delegate: self,
      cancelButtonTitle: "Hủy bỏ",
      destructiveButtonTitle: "Xóa"
    )
    ```

    Tuy nhiên, nếu tham số có 2 hoặc hơn closures, hãy chuyển xuống dòng.

    ```swift
    UIView.animate(
      withDuration: 0.25,
      animations: {
        // doSomething()
      },
      completion: { finished in
        // doSomething()
      }
    )
    ```

- Nếu câu lệnh `if let` dài, chuyển dòng và thụt lề một khoảng.

    ```swift
    if let user = self.veryLongFunctionNameWhichReturnsOptionalUser(),
       let name = user.veryLongFunctionNameWhichReturnsOptionalName(),
      user.gender == .female {
      // ...
    }
    ```

- Nếu câu lệnh `guard let` dài, chuyển dòng và thụt lề một khoảng. `else` sẽ có cùng mức thụt lề với `guard`.

    ```swift
    guard let user = self.veryLongFunctionNameWhichReturnsOptionalUser(),
          let name = user.veryLongFunctionNameWhichReturnsOptionalName(),
          user.gender == .female
    else {
      return
    }
    ```

### Chiều dài dòng tối đa

- Một dòng không được vượt quá 99 ký tự.

    Để dễ dàng kiểm tra, bạn có thể bật tính năng "Page guide at column" trong Xcode ở **Preferences → Text Editing → Display** và đặt giá trị là 99.

### Dòng trống

- Đảm bảo không có khoảng trắng trong dòng trống.
- Mọi tệp mã đều phải kết thúc bằng dòng trống.
- Thêm dòng trống trước và sau các khối `MARK`.

    ```swift
    // MARK: Layout

    override func layoutSubviews() {
      // doSomething()
    }

    // MARK: Actions

    override func menuButtonDidTap() {
      // doSomething()
    }
    ```

### Nhập khẩu

Sắp xếp các nhập khẩu theo thứ tự bảng chữ cái. Đầu tiên là các framework nội bộ, sau đó là các framework bên ngoài, tách biệt bằng dòng trống.

```swift
import UIKit

import SwiftyColor
import SwiftyImage
import Then
import URLNavigator
```

## Đặt tên

### Lớp và cấu trúc

- Sử dụng UpperCamelCase cho tên lớp và cấu trúc.
- Không thêm tiền tố vào tên lớp.

  **Ví dụ tốt:**

  ```swift
  class SomeClass {
    // class definition goes here
  }

  struct SomeStructure {
    // structure definition goes here
  }
  ```

  **Ví dụ xấu:**

  ```swift
  class someClass {
  // class definition goes here
  }

  struct someStructure {
  // structure definition goes here
  }
  ```

### Hàm

- Sử dụng lowerCamelCase cho tên hàm.
- Không nên thêm tiền tố `get` vào tên hàm.

    **Ví dụ tốt:**

    ```swift
    func name(for user: User) -> String?
    ```

    **Ví dụ xấu:**

    ```swift
    func getName(for user: User) -> String?
    ```

- Tên hàm hành động nên theo cấu trúc 'Chủ từ + Động từ + Túc từ'.

    **Ví dụ tốt:**

    ```swift
    func backButtonDidTap() {
      // ...
    }
    ```

    **Ví dụ xấu:**

    ```swift
    func back() {
      // ...
    }
    ```

### Biến

- Sử dụng lowerCamelCase cho tên biến.

### Hằng số

- Sử dụng lowerCamelCase cho tên hằng số.

    **Ví dụ tốt:**

    ```swift
    let maximumNumberOfLines = 3
    ```

    **Ví dụ xấu:**

    ```swift
    let MaximumNumberOfLines = 3
    let MAX_LINES = 3
    ```

### Liệt kê

- Sử dụng UpperCamelCase cho tên của enum.
- Sử dụng lowerCamelCase cho các case của enum.

  **Ví dụ tốt:**

  ```swift
  enum Result {
    case success
    case failure
  }
  ```

  **Ví dụ xấu:**

  ```swift
  enum Result {
    case Success
    case Failure
  }
  ```

### Giao thức

- Sử dụng UpperCamelCase cho tên giao thức.
- Khi một cấu trúc hoặc lớp tuân thủ giao thức, đặt dấu hai chấm và một khoảng trắng.

  **Ví dụ tốt:**

  ```swift
  protocol SomeProtocol {
    // protocol definition goes here
  }

  struct SomeStructure: SomeProtocol {
    // structure definition goes here
  }
  ```

### Viết tắt

- Viết tắt bắt đầu bằng chữ cái thường.
- Các từ viết tắt khác sử dụng chữ cái in hoa.

    **Ví dụ tốt:**

    ```swift
    let userID: Int?
    let html: String?
    let websiteURL: URL?
    ```

    **Ví dụ xấu:**

    ```swift
    let userId: Int?
    let HTML: String?
    let websiteUrl: NSURL?
    ```

### Delegate

- Phương thức Delegate phân biệt bằng cách sử dụng tên giao thức.

    **Ví dụ tốt:**

    ```swift
    protocol UserCellDelegate {
      func userCellDidSetProfileImage(_ cell: UserCell)
    }
    ```

    **Ví dụ xấu:**

    ```swift
    protocol UserCellDelegate {
      func didSetProfileImage()
    }
    ```

## Closures

- Định nghĩa Closure không có tham số và trả về giá trị là `() -> Void`.

    **Ví dụ tốt:**

    ```swift
    let completionBlock: (() -> Void)?
    ```

    **Ví dụ xấu:**

    ```swift
    let completionBlock: (() -> ())?
    ```

- Khi định nghĩa Closure, không cần sử dụng dấu ngoặc cho tham số.

    **Ví dụ tốt:**

    ```swift
    { operation, responseObject in
      // doSomething()
    }
    ```

    **Ví dụ xấu:**

    ```swift
    { (operation, responseObject) in
      // doSomething()
    }
    ```

## Lớp và Cấu trúc

- Sử dụng `self` rõ ràng trong các lớp và cấu trúc.
- Khi tạo cấu trúc, sử dụng trình tạo của Swift.

    **Ví dụ tốt:**

    ```swift
    let frame = CGRect(x: 0, y: 0, width: 100, height: 100)
    ```

## Kiểu

- Thay vì sử dụng `Array<T>` và `Dictionary<T: U>`, sử dụng `[T]` và `[T: U]`.

    **Ví dụ tốt:**

    ```swift
    var messages: [String]?
    var names: [Int: String]?
    ```

## Chú thích

- Sử dụng `///` cho các chú thích tài liệu.

    ```swift
    /// Người dùng sẽ hiển thị hồ sơ.
    class ProfileView: UIView {
      /// Hiển thị tên người dùng.
      var nameLabel: UILabel!
    }
    ```

- Sử dụng `// MARK:` để phân chia mã.

    ```swift
    // MARK: Layout

    override func layoutSubviews() {
      // doSomething()
    }
    ```

## Khuyến nghị lập trình

- Nếu có thể, hãy khởi tạo biến ngay khi khai báo. Sử dụng [Then](https://github.com/devxoul/Then).

    ```swift
    let label = UILabel().then {
      $0.textAlignment = .center
      $0.textColor = .black
      $0.text = "Hello, World!"
    }
    ```

- Dùng `enum` để nhóm các hằng số tương tự.

    ```swift
    private enum Metric {
      static let profileImageViewLeft = 10.f
    }
    ```

## Giấy phép

Tài liệu này có thể được sử dụng theo [Giấy phép Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/), bản quyền thuộc [Devxoul](https://github.com/devxoul) và [StyleShare](https://stylesha.re).
