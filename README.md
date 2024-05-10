# Base64エンコードの実装

以下の5つのステップでエンコードする
1. 文字列をASCIIコードに変換し, 2進数に変換する
2. 6ビットずつに分割する
3. 6の倍数にならなかったら, 0 で埋める
4. 変換表を用いて, 4文字ずつエンコードする
5. 4の倍数にならなかったら, = で埋める

ABCDという文字列を例にエンコードする
## step1
ABCDは
```
01000001 01000010 01000011 01000100
```
となる（見やすさのため, 空白を入れているが, 実際には空白は入れない）.
ASCIIコードに変換した後, 8ビットの2進数に変換する.

## step2
[stpe1](#step1)で変換した文字列を6ビットずつに分割する.
```
010000 010100 001001 000011 010001 00
```

## step3
[step2](#step2)で分割した文字列の長さは32であり, 6の倍数でない. 
<br>
したがって, 最も近い6の倍数になるように文字列の末尾に 
0 を追加する.
```
010000 010100 001001 000011 010001 000000
```

## step4
このリポジトリではbase64_table.jsonファイルが変換表である. <br>
この[変換表](https://ja.wikipedia.org/wiki/Base64#変換形式)にしたがって, [step3](#step3)で得られた文字列を6ビットずつ文字に変換する.
```
QUJD RA
```

## step5
[step4](#step4)で得られた文字列の長さは4の倍数でない. <br>
したがって, 最も近い4の倍数になるように文字列の末尾に = を追加する.
```
QUJD RA==
```


# Dockerの起動法
以下のコマンドを入力する.
```
docker compose up --build
```
