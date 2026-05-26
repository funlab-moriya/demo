# ベースイメージとして OpenJDK 21 を使用
  FROM eclipse-temurin:21-jdk-alpine
  
  # Maven をインストール
  RUN apk add --no-cache maven
  
  # 作業ディレクトリを設定
  WORKDIR /app
  
  # 依存関係を事前にダウンロード（ビルド時間短縮のため）
  COPY demo/pom.xml .
  RUN mvn dependency:go-offline -B
  
  # プロジェクトのソースコードをコピー
  COPY demo/ .
  
  # JAR ファイルを作成（テストはスキップ）
  RUN mvn clean package -DskipTests
  
  # ホットリロードを有効にする環境変数を設定
  ENV JAVA_OPTS="-Dspring.devtools.restart.enabled=true -Dspring.devtools.livereload.enabled=true"
  
  # アプリケーションの起動
  ENTRYPOINT ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar", "--spring.devtools.restart.enabled=true"]
  #ENTRYPOINT ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar", "--spring.devtools.restart.enabled=true"]