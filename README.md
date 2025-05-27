# MetaboRidgePredict
Genotype-based prediction of metabolite levels and ratios.
Usage: Rscript run_predict.R [options]

Predict metabolite expression values from genotype data using pre-trained ridge regression models.

Options:
  --input=<path>    Path to the genotype file in PLINK --recode A format (.raw).
                    This file should contain sample IDs and SNP data, where each row
                    represents an individual and columns include metadata (FID, IID, etc.)
                    followed by SNP genotypes (0, 1, 2, or NA).
                    Required.

  --id=<code>       Metabolite code (e.g., "p23400") corresponding to a pre-trained model.
                    This code must match an entry in metabo_codes.csv and a model file
                    named <code>.rds (e.g., p23400.rds) in the models/ directory.
                    Required.

  --out=<path>      Output file path for predictions (default: "predictions.csv").
                    The result will be a CSV file with two columns: "ID" (sample IDs)
                    and "Predicted_Value" (predicted expression values).
                    Optional.

  --impute=TRUE|FALSE Whether to impute missing SNPs (default: FALSE).
                    If set to TRUE, missing SNPs will be imputed using pre-defined fill values.
                    If set to FALSE, only available SNPs will be used for prediction.
                    Optional.

  --list            List all available metabolite codes and their corresponding model files.
                    This will help you choose a valid metabolite code for the --id option.
                    Optional.

  --help            Display this help message and exit.

Examples:
  Rscript run_predict.R --input=genotype_test.raw --id=p23400 --out=predictions_test.csv
  Rscript run_predict.R --list

Notes:
  - The genotype file must follow PLINK --recode A format.
  - Predictions use the lambda.1se value from the pre-trained model.
  - Ensure the package MetaboRidgePredict is installed before running.

For more information, see the package documentation or contact the maintainer.
