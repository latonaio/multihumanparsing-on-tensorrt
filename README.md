# multihumanparsing-on-tensorrt
multihumanparsing-on-tensorrt は、DeepStream 上で Multi-Human Parsing の AIモデル を動作させるマイクロサービスです。  

## 動作環境
- NVIDIA 
    - DeepStream
- Multi-Human Parsing
- Docker
- TensorRT Runtime

## Multi-Human Parsingについて
[Multi-Human Parsing](https://github.com/ZhaoJ9014/Multi-Human-Parsing) は、画像内の身体の部分や衣服のアイテムに属する意味的に一貫した領域に分割し、各ピクセルに意味的な部分のラベルと当該領域が属するIDを割り当てるAIモデルです。  
[Multi-Human Parsing](https://github.com/ZhaoJ9014/Multi-Human-Parsing) は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順
### Dockerコンテナの起動
Makefile に記載された以下のコマンドにより、Multi-Human Parsing の Dockerコンテナ を起動します。
```
docker-run: ## Docker ストリーミング用コンテナを建てる
	./docker/run.sh
```
### ストリーミングの開始
以下のコマンドにより、DeepStream 上の Multi-Human Parsing でストリーミングを開始します。  

```
segnet --network=fcn-resnet18-mhp --alpha=90 /dev/video0
```

## engineファイルについて
本レポジトリのengineファイルは、multihumanparsing-on-tensorrt/data/networks/FCN-ResNet18-MHP-512x320 にあります。  
なお、Multi-Human Parsingの NVIDIA Jetson用の engineファイルは、[jetson-inference](https://github.com/dusty-nv/jetson-inference) からダウンロードできます。  

