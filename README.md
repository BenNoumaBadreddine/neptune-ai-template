# Neptune ai platform template
## Get started
### Install neptune.ai packages
Install [neptune.ai](https://neptune.ai/). This package will help us to keep
tracking of ML experiments.

* Create a free [account](https://ui.neptune.ai/auth/realms/neptune/protocol/openid-connect/registrations?client_id=neptune-frontend&redirect_uri=https%3A%2F%2Fapp.neptune.ai%2F-%2Fonboarding&state=e18d6183-a384-42cd-8e3d-ae5738ba63b1&response_mode=fragment&response_type=code&scope=openid&nonce=2cc29941-845b-4dd4-83c1-7a6c6cd72830).

* Install Neptune client library.

      pip install neptune-client

### Template of use
    import neptune
    import os

    # Get the token for neptune ai API
    NEPTUNE_API_TOKEN = os.environ.get('NEPTUNE_API_TOKEN')

    # Initialize Neptune
    neptune.init(project_qualified_name="badreddine/sandbox", api_token=NEPTUNE_API_TOKEN)
    
    # define the parameters of the model
    PARAMS = {'features': features,
          'batch_size': 64,
          'n_epochs': 1,
          'activation': 'relu',
          'dense_units': 256,
          'optimizer': 'adam',
          'loss_metrics': 'mean_squared_error',
          'input_dim': len(features),
          'learning_rate': 0.001,
          'patience': 10,
          'validation_split': 0.2,
          'output_dim': 1
          }

    # create an experiment and log tags, name of the project, and the parameters
    with neptune.create_experiment(name='keras-integration-example', params=PARAMS,
                               tags=["temperature-forecasting", "keras-model", 'Neural-network']):

        
        # train the model for example kerasRegressor: 'estimator'
        estimator.model.summary(print_fn=lambda x: neptune.log_text('model_summary', x))

        desc = '\n'.join(['class {}: {}'.format(i, pred)
                                         for i, pred in enumerate(y_pred)])
        # log images
        neptune.log_image('predictions',
                          image,
                          description=desc)

        # log metrics results
        neptune.log_metric('accuracy', 0.95) 

        # log artifacts
        neptune.log_artifact(checkpoint_file_path) 