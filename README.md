## Danh sách thành viên nhóm 7:
1. 24521676 - Đỗ Toàn Thịnh
2. 24521656 - Trần Đình Thi
3. 24521773 - Nguyễn Hữu Tiến
4. 24521593 - Vũ Cao Thạch

Link github: https://github.com/Daruni06/group-7-campus-bookstore-lab-fixed

## Các lỗi tìm được:
 * Lỗi syntax:
1. Trong file pages/customers.php, lỗi dấu ngoặc, ngoặc vuông [ đang mở mà chưa đóng.
2. Trong file pages/reports.php, lỗi không tìm thấy biến $totalsByCategory do thiếu dấu chấm phẩy ; ở dòng trước.
3. Trong file pages/settings.php, lỗi ban đầu chỉ có chấm phẩy ; mà chưa đóng ngoặc vuông ], phải thêm vào: ];.

 * Lỗi logic: 
4. Trong file pages/dashboard.php:
```php
foreach ($orders as $order) {
   if ($order['status'] === 'pending') {
      $completedOrders++;
      $totalRevenue += calculate_order_total($order, $products);
   }
}
```
   Người code đang muốn đếm xem có bao nhiêu đơn đã hoàn thành, nhưng lại chọn những đơn hàng "pending" để đếm.  
   Cách sửa: sửa 'pending' thành 'completed'.  
```php
foreach ($orders as $order) {
   if ($order['status'] === 'completed') {
      $completedOrders++;
      $totalRevenue += calculate_order_total($order, $products);
   }
}
```

5. Trong file pages/reports.php:
```php
foreach ($products as $product) {
   $category = $product['name'];
...
```
   Đang kiểm tra category mà lại đi check name của product.  
   Cách sửa: sửa 'name' thành 'category'.  
```php
foreach ($products as $product) {
   $category = $product['category'];
...
```
6. Trong file data/customers.php:
```php
   'name' => 'Linh Pham',
   'email' => 'linh@student.example.com',
   'tier' => 'faculty',
   'active' => true,
```
   Khách hàng Linh Pham đang có email student nhưng tier lại là faculty.  
   Cách sửa: sửa từ tier 'faculty' thành 'student'.  
```php
   'name' => 'Linh Pham',
   'email' => 'linh@student.example.com',
   'tier' => 'student',
   'active' => true,
```
7. Trong file pages/orders.php:
```php
   foreach ($orders as $order) {
      if ($order['status'] === 'completed') {
         $pendingOnly[] = $order;
      }
   }
``` 
   Người code đang muốn đưa các order với status 'pending' vào $pendingOnly nhưng lại xét các order có status là 'completed'.  
   Cách sửa: sửa status của $order thành 'pending'.  
```php
   foreach ($orders as $order) {
      if ($order['status'] === 'pending') {
         $pendingOnly[] = $order;
      }
   }
```
8. Trong file pages/checkout.php:
```php
   $cart = [
      ['sku' => 'BK-101', 'qty' => 2],
      ['sku' => 'PN-301', 'qty' => 5],
   ];

   $subtotal = 0;

   foreach ($cart as $item) {
      $subtotal = $products[$item['sku']]['price'] * $item['qty'];
   }
```
   Trong giỏ hàng đang có 2 đơn, nhưng tổng $subtotal lại chỉ tính có 1 do đang gán bởi dấu bằng =.  
   Cách sửa: thay dấu = thành += để cộng tổng tất cả các đơn trong $cart.  
```php
   $cart = [
      ['sku' => 'BK-101', 'qty' => 2],
      ['sku' => 'PN-301', 'qty' => 5],
   ];

   $subtotal = 0;

   foreach ($cart as $item) {
      $subtotal += $products[$item['sku']]['price'] * $item['qty'];
   }
```
