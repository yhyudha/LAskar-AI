def create_rfm_df(df):
    rfm_df = df.groupby(by="customer_id", as_index=False).agg({
        "order_date": "max",         # ambil tanggal order terakhir
        "order_id": "nunique",       # hitung jumlah order unik (frequency)
        "total_price": "sum"         # total belanja (monetary)
    })
    rfm_df.columns = ["customer_id", "max_order_timestamp", "frequency", "monetary"]
    
    # Konversi timestamp jadi date (tanpa jam)
    rfm_df["max_order_timestamp"] = rfm_df["max_order_timestamp"].dt.date

    # Cari tanggal order terakhir secara keseluruhan
    recent_date = df["order_date"].dt.date.max()

    # Hitung recency (jumlah hari sejak order terakhir)
    rfm_df["recency"] = rfm_df["max_order_timestamp"].apply(
        lambda x: (recent_date - x).days
    )

    # Hapus kolom timestamp karena sudah dipakai
    rfm_df.drop("max_order_timestamp", axis=1, inplace=True)
    
    return rfm_df
