# chrisshop.com38167
 #!/bin/bash
# deploy_web_Token.sh
# Script to deploy website with API Token to Google Cloud Run

PROJECT_ID="chrisshop.com38167"
SERVICE_NAME="chrisshop.com38167"
REGION="asia-southeast1"
API_TOKEN_VALUE="YourSecretTokenHere"

echo "🚀 Starting deployment for $SERVICE_NAME ..."

# 1. Set project
gcloud config set project $PROJECT_ID

# 2. Enable necessary APIs
echo "📡 Enabling Google Cloud APIs..."
gcloud services enable run.googleapis.com \
    artifactregistry.googleapis.com \
    cloudbuild.googleapis.com

# 3. Deploy service to Cloud Run
echo "📦 Deploying to Cloud Run..."
gcloud run deploy $SERVICE_NAME \
    --source . \
    --region $REGION \
    --allow-unauthenticated

# 4. Set API Token as environment variable
echo "🔑 Setting API Token..."
gcloud run services update $SERVICE_NAME \
    --region $REGION \
    --set-env-vars MY_API_TOKEN="$API_TOKEN_VALUE"

# 5. Get Service URL
SERVICE_URL=$(gcloud run services describe $SERVICE_NAME --region $REGION --format 'value(status.url)')

echo "✅ Deployment complete!"
echo "🌍 Website: $SERVICE_URL"
echo "🔑 Token Endpoint: $SERVICE_URL/api/token"
gcloud run services update chrisshop.com38167\
  --region asia-southeast1 \
  --set-env-vars MY_API_TOKEN="YourSecretTokenHere"
  
  gcloud logs read --project=chrisshop.com38167
  🌍 Website URL: https://chrisshop.com38167-web-xxxxx.a.run.app
🔑 Your API Token: YourSecretTokenHere
🔗 Token-protected Endpoint: https://chrisshop.com/.a.run.app/api/token
