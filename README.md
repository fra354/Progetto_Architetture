# Progetto_Architetture:: gli ID nelle versioni 64 e 64omp vengono per errore salvati a 8 byte
dovete chiamare, per salvare gli ID in queste due versioni la funzione
 

void save_int_data(char* filename, int* X, int n, int k) {
	FILE* fp;
	int i;
	fp = fopen(filename, "wb");
	if(X != NULL){
		fwrite(&n, 4, 1, fp);
		fwrite(&k, 4, 1, fp);
		for (i = 0; i < n; i++) {
			fwrite(X, sizeof(int), k, fp);
			//printf("%i %i\n", ((int*)X)[0], ((int*)X)[1]);
			X += sizeof(int)*k;
		}
	}
	else{
		int x = 0;
		fwrite(&x, 4, 1, fp);
		fwrite(&x, 4, 1, fp);
	}
	fclose(fp);
}
