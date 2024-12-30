# Image Retrieval Model Analysis

## Retrieval Results Comparison

Different models were evaluated for their retrieval performance using various recall metrics:

| Model | Recall@1 | Recall@2 | Recall@3 | Recall@5 | Recall@10 |
|-------|----------|----------|----------|----------|-----------|
| resnet18_embedding | 0.246589 | 0.309608 | 0.349768 | 0.400971 | 0.468350 |
| resnet50_embedding | 0.258335 | 0.324378 | 0.363131 | 0.414545 | 0.485019 |
| mobilenetv3_embedding | 0.319595 | 0.392179 | 0.436208 | 0.489309 | 0.555493 |
| vit_embedding | 0.329020 | 0.413349 | 0.459769 | 0.520467 | 0.594528 |
| efficientnet_embedding | 0.347025 | 0.423266 | 0.468280 | 0.521030 | 0.591715 |
| resnet50_finetuned | 0.358982 | 0.461176 | 0.519342 | 0.593192 | 0.685188 |
| clip_embedding | 0.454354 | 0.555141 | 0.611971 | 0.672457 | 0.743002 |
| clip_finetuned | 0.621255 | 0.719862 | 0.769518 | 0.822197 | 0.873822 |
| unicom | 0.861865 | 0.909481 | 0.930089 | 0.949079 | 0.967084 |

## Dataset and References

- **Evaluation Dataset**: [DeepFashion In-Shop Retrieval Dataset](https://mmlab.ie.cuhk.edu.hk/projects/DeepFashion/InShopRetrieval.html)
- **Reference Paper**: [UNICOM Paper](https://arxiv.org/pdf/2304.05884v1)

## Methodology and Approach

1. Evaluated retrieval efficiency across various embedding models (small to large)
2. Selected UNICOM model as teacher based on research paper and superior retrieval efficiency
3. Conducted transfer learning experiments:
   - Finetuned projection layer in ResNet50 and CLIP-ViT32 for 10 epochs
   - Demonstrated successful transfer learning with improved efficiency
4. Motivation for transfer learning: UNICOM model size (1.6GB) necessitated smaller models for reduced latency

## Dimensionality Reduction Analysis

Performance of UNICOM model with reduced embedding dimensions:

| Model | Recall@1 | Recall@2 | Recall@3 | Recall@5 | Recall@10 |
|-------|----------|----------|----------|----------|-----------|
| unicom | 0.861865 | 0.909481 | 0.930089 | 0.949079 | 0.967084 |
| unicome_512 | 0.860670 | 0.907582 | 0.929245 | 0.947883 | 0.964974 |
| unicome_384 | 0.859122 | 0.907160 | 0.928823 | 0.946898 | 0.965748 |
| unicome_256 | 0.852933 | 0.904065 | 0.924954 | 0.944929 | 0.963567 |
| unicome_128 | 0.840906 | 0.890561 | 0.914053 | 0.937474 | 0.956393 |
| unicome_96 | 0.832255 | 0.883739 | 0.908285 | 0.931144 | 0.951540 |
| unicome_64 | 0.808975 | 0.865804 | 0.893093 | 0.918765 | 0.944015 |
| unicome_24 | 0.658109 | 0.740962 | 0.778661 | 0.818821 | 0.862217 |

## Key Findings and Recommendations

1. **Embedding Dimensions Impact**:
   - Lower dimension embeddings can significantly improve system speed
   - Performance remains relatively stable until significant dimension reduction

2. **Recommended Approach**:
   - Use lower-dimensional embeddings for initial candidate retrieval
   - Apply higher-dimensional embeddings for reranking
   - This approach is applicable to smaller models finetuned on UNICOM

3. **Transfer Learning Viability**:
   - Successfully demonstrated with ResNet50 and CLIP-ViT32
   - Provides a practical compromise between model size and performance
