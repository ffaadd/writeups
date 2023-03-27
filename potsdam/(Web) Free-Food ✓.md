Man muss `state` auf `10000` erhöhen um die Flagge zu bekommen. 
Wenn man `/api/giveaway/participate` aufruft, erhöht sich state um 1.
Die aufrufende IP wird für 1 Std gesperrt.
Der Host vertraut auf das `X-Forwarded-For` Headerfeld, damit kann man die IP-Adresse faken und so state schnell auf `10000` erhöhen. Sobald dies erreicht ist wird die Flagge als `coupon` mitgeliefert.