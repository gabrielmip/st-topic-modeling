A execução do DREx foi dividida em duas partes.

Na primeira, ocorre a criação do arquivo de cache.
Esse arquivo deve ser criado para cada base a ser expandida.
A execução é a seguinte

	python create_cache.py -i <dataset_file> -v <words_vector> -l <n-gram> -n <number_similar_words> -c <output_cache_filename>

	-i: Dataset com os documentos. Um documento por linha no formato csv. No csv podem existir quantas colunas forem necessárias com a restrição de que o texto do documento fique na ultima coluna. Ex.:

		doc1_ID,doc1_feature1,doc1_feature2, … , doc1_featureN, doc1_text
		doc2_ID,doc2_feature1,doc2_feature2, … , doc2_featureN, doc2_text
		…
		docN_ID,docN_feature1,docN_feature2, … , docN_featureN, docN_text

	-v: Arquivo com o modelo de vetores de palavras no formato word2vec:

		numero_palavras numero_dimensões 
		palavra1 valor1 valor2 valor3 … 
		palavra2 valor1 valor2 valor3 … 

	-l: Tamanho do ngrama. 1 = unigrama, 2 = bigrama, 3 = trigrama …

	-n: Numero de palavras similares a cada ngrama que será salvo na cache. Este valor em geral é alto (200 ~ 1000). Atenção, valores muito altos vão fazer o arquivo de cache ficar muito grande

	-c: Arquivo onde a cache será salva.


Na segunda parte ocorre a expansão dos documentos:

	python expand.py -i <dataset_file> [-s] -v <expansion_values> -l <n-gram> -c <cache_file> -o <output_path> -f <output_files_prefix> [-p]

	-i:  Dataset com os documentos. Um documento por linha no formato csv. No csv podem existir quantas colunas forem necessárias com a restrição de que o texto do documento fique na ultima coluna. Ex.:

		doc1_ID,doc1_feature1,doc1_feature2, … , doc1_featureN, doc1_text
		doc2_ID,doc2_feature1,doc2_feature2, … , doc2_featureN, doc2_text
		…
		docN_ID,docN_feature1,docN_feature2, … , docN_featureN, docN_text

	-s: Opcional. Se essa flag for usada o DREx irá expandir os documentos utilizando scaling factors. Se não for utilizada os documentos serão expandidos até atingirem um tamanho fixo.

	-v: Lista de valores (separada por virgulas) que controlam o tamanho final dos arquivos após a expansão. Se -s for setado, esses valores são interpretados como scaling factors, caso contrario determinam os tamanhos finais dos documentos. Note que será criado um arquivo de saída para cada valor passado.

	-l : Tamanho do ngrama. 1 = unigrama, 2 = bigrama, 3 = trigrama … (deve ser o mesmo informado na criação da cache)

	-c: Arquivo que contém a cache salva.

	-o: pasta onde os arquivos de saída serão salvos

	-f: prefixo dos nomes dos arquivos de saída.

	-p: Opcional. Se essa flag for passada a seleção das palavras candidatas será probabilística. Caso contrario a seleção será top n.



