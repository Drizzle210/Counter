Vào settings của repository muốn force signature commits, vào Branches -> Branch protection rules -> Add branch protection rule và tích vào Require signed commits để enable tính năng check signature commits. Private repos của org cần upgrade lên Team / Enterprise mới dùng được

Install GPG (Mặc định Linux đã có sẵn, còn các OS khác phải cài) - https://www.gnupg.org/download/

MacOS / Windows có thể có bản Desktop dễ dùng hơn. Nếu có thì dùng theo UI. Còn muốn dùng qua CLI thì follow tiếp bên dưới

Generate key local: gpg --full-generate-key --expert
Chọn ECC and ECC, rồi chọn Ed25519 để tăng tính bảo mật (không dùng RSA) và làm theo hướng dẫn

Lấy GPG key ID: gpg --list-secret-keys --keyid-format=long
Định dạng key ID: 3AA5C34371567BD2

------------------------------------
sec   ed25519/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
uid                          Hubot 
ssb   cv25519/42B317FD4BA89E7A 2016-03-10
Lấy public key: gpg --armor --export 3AA5C34371567BD2
và submit GPG public key lên github account: https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account#adding-a-gpg-key

Set GPG key ID cho local Github: git config --global user.signingkey 3AA5C34371567BD2

Set sign commits global: git config --global commit.gpgsign true

Khi commit thì thêm flag -S (hình như chỉ cần 1 lần đầu khi commit): git commit -S -m "your commit message"

Reference: https://gist.github.com/ducphamle2/36bfc744d47183344d2b4c44d9c41b2f