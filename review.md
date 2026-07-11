Review 1
Questions
1. Summary: In 3–7 sentences, describe the key ideas, experimental or theoretical results, and their significance.
The paper proposes SLMambaMedseg, a medical image segmentation framework that combines Vision Mamba-based global feature modeling with strip and large-kernel convolution modules for capturing thin or elongated structures. It is evaluated on Synapse and ACDC and reports competitive segmentation results, including Synapse Dice/HD95 and organ-level Dice scores. The method shows improvements over TransCASCADE on Synapse and includes ablations for the encoder, SLGAG, and kernel strategy. The idea is relevant and potentially useful, but the experimental evidence is weakened by inconsistent reported results, limited reproducibility details, incomplete efficiency evidence, and insufficient module-level ablation.
2. Strengths: Consider the significance of the key ideas, the experimental or theoretical validation, the writing quality, and the data contribution. Clearly explain why these aspects of the paper are valuable. Short bullet lists are Not sufficient.
Timely topic in medical image segmentation, reasonable use of Vision Mamba for global feature modeling, useful strip/large-kernel convolution idea for thin and elongated organs, evaluation on two public datasets, Synapse and ACDC, reports Dice and HD95 on Synapse, reports organ-level Dice scores, achieves competitive Synapse results of 83.36 Dice and 16.18 HD95 in Table 1, reports strong ACDC Dice of 93.51 in Table 2, shows improvement over TransCASCADE on Synapse Dice from 82.68 to 83.36 and HD95 from 17.34 to 16.18, includes ablation on encoder type, SLGAG, and kernel strategy.
3. Weaknesses: Consider the significance of the key ideas, the experimental or theoretical validation, the writing quality, and the data contribution. Clearly explain why these aspects are weaknesses of the paper, e.g., why a specific prior work has already demonstrated the key contributions, or why the experiments are insufficient to validate the claims, etc. Short bullet lists are NOT sufficient.
Novelty is not clearly established; proposed modules look like combinations of existing Mamba, U-Net decoder, CBAM-style attention, strip convolution, large-kernel convolution, and depthwise convolution ideas. The SOTA claim is not fully convincing because the numerical gains are small; efficiency is repeatedly claimed, but no FLOPs, parameter count, GPU memory, inference speed, or training time is reported; the experimental protocol is incomplete; the baseline comparison is not clearly fair; no repeated runs or standard deviation are provided; no statistical significance test is reported; ablation is too limited for a model with many components; the contribution of CA, SA, SC, MA, SLCB, Dice loss, and Focal loss is not separately verified; and writing quality and technical presentation need major revision.

Manuscript-level concerns: Synapse Dice is inconsistent because Table 1 reports 83.36 while the text states 83.56, ACDC result is inconsistent because Table 2 reports 93.51 while the text and Table 3 report 92.81, Table 3 reports SLMambaMedseg as 83.36 Dice / 16.18 HD95 on Synapse and 92.81 Dice on ACDC, but this conflicts with Table 2, the claimed improvement over TransCASCADE on ACDC is unclear because Table 2 shows 93.51 vs 92.12 but Table 3 uses 92.81, SLGAG ablation improves Synapse Dice from 81.80 to 83.36 and ACDC Dice from 90.79 to 92.81, but no deeper module-level ablation is provided, left-kidney Dice improves from 83.97 to 88.57 with SLGAG but this single-organ gain is not sufficiently analyzed, kernel strategy [1,3,5] gives the best Synapse Dice of 83.36 and ACDC Dice of 92.81, but the reason is only weakly discussed, abstract module names MSLCB and SLGA are inconsistent with main-text names SLCB and SLGAG, figures wrongly mention “polyps” for Synapse organ segmentation and ACDC cardiac segmentation, ACDC discussion refers to the wrong figure number, dataset splits are not clearly stated, preprocessing details are incomplete, patient-level separation is not explained, random seed and number of runs are missing, loss-function parameters such as Focal Loss alpha/gamma and Dice smoothing are not reported, VSS and SLGAG equations are not fully clear, SLCB is not mathematically well defined, important recent Mamba-based medical segmentation works are missing, conclusion overstates the evidence by claiming broader superiority of Vision Mamba without enough support.
4. Paper Rating
Weak Reject
5. Reviewer Experience in Subject Area
Informed
6. Justification of Rating: What are the most important factors in your rating?
The Weak Reject rating reflects that the topic is relevant and the proposed idea has some value, but the current manuscript is not reliable enough for acceptance. The most important factors are the unclear novelty over closely related work, the incomplete experimental protocol, the missing statistical validation, the insufficient ablation, and the unsupported or inconsistent claims. Although the paper reports competitive results in some settings, the evidence is not strong enough to support the stated conclusions without major corrections, stronger baselines, reproducibility details, and more rigorous validation.
7. Additional Comments to Author(s): Include any comments that may be useful for revision but should not be considered in the paper decision.
• Reconcile all inconsistent reported results, especially Synapse Dice 83.36 versus 83.56 and ACDC Dice 93.51 versus 92.81.
• Clearly state dataset splits, preprocessing, patient-level separation, random seeds, number of runs, and baseline implementation details.
• Report FLOPs, parameter count, GPU memory, inference speed, and training time to support the efficiency claim.
• Add separate ablations for CA, SA, SC, MA, SLCB, SLGAG, dice loss, and focal loss, including loss hyperparameters.
• Correct figure labels, such as the inappropriate use of "polyps"; fix figure numbering; improve equations; and add missing recent Mamba-based medical segmentation references.


Review 2
Questions
1. Summary: In 3–7 sentences, describe the key ideas, experimental or theoretical results, and their significance.
This article proposes a medical image segmentation framework called SLMambaMedseg. The core idea is to combine the Vision Mamba (VSS) encoder with a decoder based on multi-scale strip-shaped large kernel convolution.
The main innovation points include: (1) using VSS Block as an encoder, utilizing its linear computational complexity to achieve global context modeling; (2) Designed a new decoder module SLCB (integrated channel attention CA, spatial attention SA, stripe convolution SC, multi-scale attention MA); (3) Introducing SLGAG (Striped Large Kernel Group Attention Gated Mechanism) at the skip connection using a mixed loss function of Soft Dice Loss and Focal Loss.
This method was compared with multiple methods on the Synapse and ACDC datasets, claiming to achieve SOTA performance (Synapse: DSC 83.36%, HD95 16.18; ACDC: DSC 92.81%).
2. Strengths: Consider the significance of the key ideas, the experimental or theoretical validation, the writing quality, and the data contribution. Clearly explain why these aspects of the paper are valuable. Short bullet lists are Not sufficient.
1. The direction of the topic is valuable - applying Vision Mamba to medical image segmentation is currently a hot topic.
2. Conducted comprehensive comparative experiments on two mainstream datasets.
3. Provided visual results, intuitively demonstrating the segmentation effect.
4. The ablation experiment validated the effectiveness of encoder selection, SLGAG module, and multi-scale strategy.
3. Weaknesses: Consider the significance of the key ideas, the experimental or theoretical validation, the writing quality, and the data contribution. Clearly explain why these aspects are weaknesses of the paper, e.g., why a specific prior work has already demonstrated the key contributions, or why the experiments are insufficient to validate the claims, etc. Short bullet lists are NOT sufficient.
1. The manuscript lacks sufficient novelty and its core contributions are weak. Its so-called 'core innovation' is essentially an integration of existing modules into a single architecture: VSS Block (from VMamba/Vision Mamba), CA and SA modules (from CBAM), Strip Pooling, Large Kernel Convolution (ConvNeXt), and Channel Shuffle (ShuffleNet). It lacks original structural design or theoretical innovation, reading more like a paper on 'module engineering.' Reviewers would find it hard to accept the claim of 'first dedicated integration,' as hybrid Mamba + CNN architectures (e.g., VM-UNet) have already been explored in prior work.
2. Insufficient experimental setup and training details:
Unclear data split: The commonly used split scheme for the Synapse dataset (30 cases for training / 10 cases for testing) is not explicitly stated.
Missing baseline comparison: Although nnU-Net is cited in the literature, it is entirely absent from the experimental comparison table. As nnU-Net is widely recognized as a strong baseline in medical image segmentation, omitting its comparison is a significant oversight that severely undermines the credibility of the claimed SOTA performance.
3. Insufficient ablation study: The ablation experiments are limited to only three aspects: encoder type (CNN vs. Transformer vs. Mamba), the presence of SLGAG (with/without), and the kernel size combinations of the MA module. Ablations for critical components are missing. Specifically, the necessity of Strip Convolution (SC), the role of the CA/SA attention modules, and the contribution of Large Kernel Convolution (LKC) have not been individually validated. Consequently, the claim that "each component contributes to the performance" is not adequately supported.
4. Paper Rating
Weak Reject
5. Reviewer Experience in Subject Area
Knowledgeable (Published in Area)
6. Justification of Rating: What are the most important factors in your rating?
The depth of innovation in methods, as well as the details and completeness of experiments.


Review 3
Questions
1. Summary: In 3–7 sentences, describe the key ideas, experimental or theoretical results, and their significance.
This paper proposes SLMambaMedseg, a U-shaped medical image segmentation model combining a Vision Mamba encoder with a multi-scale strip large-kernel convolutional decoder. It introduces SLCB for decoder feature refinement and SLGAG for skip-connection fusion. Experiments on Synapse and ACDC report better Dice/HD95 results than several CNN-, Transformer-, and Mamba-based baselines. The idea is relevant and the results are promising, but the current evidence is weakened by inconsistent reported numbers and insufficient experimental details.
2. Strengths: Consider the significance of the key ideas, the experimental or theoretical validation, the writing quality, and the data contribution. Clearly explain why these aspects of the paper are valuable. Short bullet lists are Not sufficient.
The paper studies an important problem in medical image segmentation: combining global context modeling with local boundary/detail preservation. The Mamba encoder plus convolutional decoder design is reasonable, especially for small or elongated anatomical structures.

The method is evaluated on two common public benchmarks, Synapse and ACDC, and compared with several representative baselines. The reported results are competitive, and the qualitative examples suggest improved segmentation of some challenging regions.

The paper includes useful ablation studies on encoder choice, SLGAG, and kernel-size strategies. These experiments provide some support for the proposed design, although they are not yet complete.
3. Weaknesses: Consider the significance of the key ideas, the experimental or theoretical validation, the writing quality, and the data contribution. Clearly explain why these aspects are weaknesses of the paper, e.g., why a specific prior work has already demonstrated the key contributions, or why the experiments are insufficient to validate the claims, etc. Short bullet lists are NOT sufficient.
The reported results contain important inconsistencies. For ACDC, Table 2 reports 93.51 Dice, while the text and Table 3 report 92.81. The class-wise average in Table 2 also does not match either value. For Synapse, the text reports 83.56 Dice, while Table 1 reports 83.36. These inconsistencies reduce confidence in the empirical claims.

The paper claims improved efficiency, but does not report parameters, FLOPs, memory usage, inference speed, or training time. Therefore, the efficiency claim is not sufficiently supported.

The novelty is somewhat incremental. The architecture combines several existing ideas, including VMamba/VSS blocks, U-shaped decoding, attention gates, strip convolutions, and large-kernel convolutions. The paper should better clarify what is genuinely new.

The experimental protocol lacks important details, including dataset splits, random seeds, number of runs, standard deviations, and whether baselines were reproduced under the same setting. The ablation study also does not isolate all major components of SLCB.

The writing needs improvement. There are grammar issues, inconsistent terms such as SLCB/MSLCB and SLGA/SLGAG, and inaccurate figure captions referring to "polyps" in non-polyp datasets.
4. Paper Rating
Weak Reject
5. Reviewer Experience in Subject Area
Informed
6. Justification of Rating: What are the most important factors in your rating?
The paper has a reasonable idea and promising results, but the current submission is not rigorous enough for acceptance. The main concerns are inconsistent quantitative results, unsupported efficiency claims, incomplete experimental protocol, and insufficient component-level ablations.
7. Additional Comments to Author(s): Include any comments that may be useful for revision but should not be considered in the paper decision.
Please carefully correct all reported numbers and make the tables consistent with the text. Please add efficiency comparisons such as parameters, FLOPs, memory, and inference time. Please clarify dataset splits, training settings, random seeds, and whether baselines are reproduced or cited. More detailed ablations of SLCB components would also strengthen the paper. The writing and figure captions should be carefully revised.