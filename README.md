This Kmeans model has been trained with l2-normalized electricity consumption data from ASM. The instructions below are meant to guide you through deploying the model on a server with MLFlow. They also contain an example of how to use the model after deployment. Consult the clusterCenters.png file for a visual representation of each of the 12 clusters.
Instructions:
1. Set up a new virtual environment with: python3 -m venv .venv
2. Activate virtual environment: ./venv/bin/activate
3. Install requirements: pip3 install -r requirements.txt
4. Serve the model. It will be listening on port 4000:
mlflow models serve -m kmeansEuclidean12 --no-conda -p 4000
5. Use curl to query the model. It should receive a JSON file containing an array of 1x24 vectors (which correspond to time series of normalised electricity consumption) and respond by assigning each time series to a cluster

Example Query:

curl http://127.0.0.1:4000/invocations -H 'Content-Type: application/json' -d '{"inputs": [[0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.1354716821903498, 0.3935744688045296, 0.46222493205905163, 0.42077999460368204, 0.40343804111067944, 0.03816305794295266, 0.09221543418398288, 0.09583805528477521, 0.30921402493063427, 0.22870934114079539, 0.14969316007927091, 0.14372121539230384, 0.11081275142363932, 0.1159059414879889, 0.11011333447772179, 0.11230125415409159, 0.11267786327799414]]}'

Response: 
[0]
