# Intel Image Classification

Bu proje, **Intel Image Classification** veri seti üzerinde çok sınıflı görüntü sınıflandırması yapmak için hazırlanmıştır. Veri setinde 6 farklı sınıf bulunuyor: **Buildings, Forest, Glacier, Mountain, Sea, Street**. Amaç, bir CNN tabanlı model ile bu görüntüleri doğru sınıflandırmaktır.

## Veri Seti
- Kaynak: [Intel Image Classification Dataset](https://www.kaggle.com/datasets/puneet6060/intel-image-classification)  
- Eğitim seti: ~25.000 görüntü  
- Test seti: ~14.000 görüntü  
- Görseller farklı boyutlarda olduğundan hepsi aynı boyuta (150x150) ölçeklendirildi.  
- Normalizasyon ve basit veri artırma teknikleri (rotation, horizontal flip) uygulandı.

## Yöntem
Proje kapsamında birkaç farklı yaklaşım denendi:

1. **Temel CNN modeli**  
   - Conv2D + MaxPooling katmanları  
   - Dropout ile overfitting azaltma  
   - Dense katman ve Softmax çıkış  

2. **Transfer Learning**  
   - ResNet50 ve MobileNetV2 gibi önceden eğitilmiş ağlar kullanıldı  
   - Kendi veri setimiz üzerinde fine-tuning yapıldı  

Eğitim sırasında **Adam optimizer** ve **categorical cross-entropy loss** kullanıldı. Erken durdurma ve öğrenme oranı azaltma callback’leri ile modelin daha stabil öğrenmesi sağlandı.

## Sonuçlar
- Basit CNN modeli ile test doğruluğu: **%85**  
- MobileNetV2 ile test doğruluğu: **%91**  
- En çok karıştırılan sınıflar: *Mountain* ↔ *Glacier*  
- Grad-CAM görselleştirmeleri, modelin özellikle sahneye ait belirgin bölgeleri (örneğin deniz ufku, yol dokusu) dikkate aldığını gösterdi.

## Yorum
Transfer learning kullanımı, basit CNN’e kıyasla daha yüksek doğruluk sağladı. Veri artırma teknikleri modelin genelleme gücünü artırdı. Ancak bazı sınıflarda (özellikle Glacier ve Mountain) görsellerin birbirine çok benzemesi nedeniyle hata oranı yüksek kaldı.

## Kaggle
Notebook’un tam sürümü Kaggle üzerinde mevcuttur:  
[[Kaggle notebook](https://www.kaggle.com/code/bardrek/image-classification)]  
