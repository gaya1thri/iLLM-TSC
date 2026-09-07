# iLLM-TSC: Integration reinforcement learning and large language model for traffic signal control policy improvement

## [Paper](https://arxiv.org/abs/2407.06025) | [Simulation](https://github.com/Traffic-Alpha/TransSimHub) |
## iLLM-TSC's powerful capabilities

https://github.com/Traffic-Alpha/TSC-HARLA/assets/75999557/92d6ff7f-cc5b-42ba-9feb-046022e70ad9



## Info
We propose a framework that utilizes LLM to support RL models. This framework refines RL decisions based on real-world contexts and provides reasonable actions when RL agents make erroneous decisions. 

<div align=center>
<img width="90%" src="./assets/iLLM-Framework.png" />

The detailed structure of iLLM-TSC.
</div>


## Typical Cases

- Case1: LLM think that the action taken by the RL Agent was unreasonable and gave a reasonable explanation and recommended actions.
<div align=center>
<img width="90%" src="./assets/Case1.png" />


</div>

- Case 2: LLM considers that the movement made by the RL Agent is not the movement with the highest current mean occupancy but it is reasonable, after which LLM gives an explanation and recommendation.
<div align=center>
<img width="90%" src="./assets/Case2.png" />
</div>

- Case 3: An ambulance needs to pass through the intersection, but the RL Agent does not take into account that the ambulance needs to be prioritized. LLM modifies the RL Agent’s action to prioritize the ambulance to pass through the intersection.
<div align=center>
<img width="90%" src="./assets/Case3.png" />
</div>

## Install

### Install [TransSimHub](https://github.com/Traffic-Alpha/TransSimHub)
The simulation environment we used is TransSimHub, which is based on SUMO and can be used for TSC, V2X and UAM simulation. More information is available via [docs](https://transsimhub.readthedocs.io/en/latest/).

You can install TransSimHub by cloning the GitHub repository. Follow these steps:
```bash
git clone https://github.com/Traffic-Alpha/TransSimHub.git
cd TransSimHub
pip install -e .
```

After the installation is complete, you can use the following Python command to check if TransSimHub is installed and view its version:

```bash
import tshub
print(tshub.__version__)
```

###  Install HARLA
You can install HARLA by cloning the GitHub repository. Follow these steps:
```bash
git clone https://github.com/Traffic-Alpha/iLLM-TSC
cd iLLM-TSC
pip install -r requirements.txt
```
After completing the above ``Install steps``, you can use this program locally. 
## Run HARLA locally
### Train RL
The first thing you need to do is train a RL model. You can do it with the following code:
```bash
cd iLLM-TSC
python sb3_ppo.py
```
The training results are shown in the figure, and model weight has been uploaded in [models](./models/). 

<div align=center>
<img width="70%" src="./assets/train_result.png" />
</div>

The effect of the RL model can be tested with the following code:
```bash
python eval_rl_agent.py
```
### Try RL+LLM
Before you can use LLM, you need to have your own KEY and fill it in the [``utils/config.yaml``](./utils/config.yaml). 
```bash
OPENAI_PROXY: 
OPENAI_API_KEY:
```
The entire framework can be used with the following code.
```bash
python rl_llm_tsc.py
```


**Evaluation Rule: To make fair evaluation and comparison among different models, make sure you use the same LLM evaluation model (we use GPT4) for all the models you want to evaluate. Using a different scoring model or API updating might lead to different results.**

## Citation

If you find our work useful in your research, we would be grateful if you could cite our papers:

```BibTeX
@article{wang2024llm,
  title={LLM-Assisted Light: Leveraging Large Language Model Capabilities for Human-Mimetic Traffic Signal Control in Complex Urban Environments},
  author={Wang, Maonan and Pang, Aoyu and Kan, Yuheng and Pun, Man-On and Chen, Chung Shue and Huang, Bo},
  journal={arXiv preprint arXiv:2403.08337},
  year={2024}
}

@inproceedings{wang2025vlmlight,
 author = {Wang, Maonan and Chen, Yirong and Pang, Aoyu and Cai, Yuxin and Chen, Chung Shue and Kan, Yuheng and Pun, Man On},
 booktitle = {Advances in Neural Information Processing Systems},
 editor = {D. Belgrave and C. Zhang and H. Lin and R. Pascanu and P. Koniusz and M. Ghassemi and N. Chen},
 pages = {39590--39621},
 publisher = {Curran Associates, Inc.},
 title = {{VLMLight}: Safety-Critical Traffic Signal Control via Vision-Language Meta-Control and Dual-Branch Reasoning Architecture},
 url = {https://proceedings.neurips.cc/paper_files/paper/2025/file/3849b5861dcaeaf4758eef0979a98cc6-Paper-Conference.pdf},
 volume = {38},
 year = {2025}
}

@ARTICLE{pang2026illmtsc,
  author={Pang, Aoyu and Wang, Maonan and Pun, Man-On and Chen, Chung Shue and Xiong, Xi},
  journal={IEEE Transactions on Vehicular Technology}, 
  title={iLLM-TSC: Integration Reinforcement Learning and Large Language Model for Traffic Signal Control Policy Improvement}, 
  year={2026},
  volume={75},
  number={8},
  pages={15762-15776},
  doi={10.1109/TVT.2026.3674284}
}
```

You may also be interested in our earlier work on RL-based traffic signal control:

```BibTeX
@ARTICLE{wang2024unitsa,
  author={Wang, Maonan and Xiong, Xi and Kan, Yuheng and Xu, Chengcheng and Pun, Man-On},
  journal={IEEE Transactions on Vehicular Technology}, 
  title={UniTSA: A Universal Reinforcement Learning Framework for V2X Traffic Signal Control}, 
  year={2024},
  volume={73},
  number={10},
  pages={14354-14369},
  doi={10.1109/TVT.2024.3403879}
}

@ARTICLE{wang2024ccda,
  author={Wang, Maonan and Chen, Yirong and Kan, Yuheng and Xu, Chengcheng and Lepech, Michael and Pun, Man-On and Xiong, Xi},
  journal={IEEE Transactions on Intelligent Transportation Systems}, 
  title={Traffic Signal Cycle Control With Centralized Critic and Decentralized Actors Under Varying Intervention Frequencies}, 
  year={2024},
  volume={25},
  number={12},
  pages={20085-20104},
  doi={10.1109/TITS.2024.3462153}
}

@ARTICLE{pang2024delaytsc,
  author={Pang, Aoyu and Wang, Maonan and Chen, Yirong and Pun, Man-On and Lepech, Michael},
  journal={IEEE Open Journal of Vehicular Technology}, 
  title={Scalable Reinforcement Learning Framework for Traffic Signal Control Under Communication Delays}, 
  year={2024},
  volume={5},
  pages={330-343},
  doi={10.1109/OJVT.2024.3368693}
}
```


## Acknowledgment

- **Yufei Teng**: Thanks for editing the video.
- **Thank you to everyone who pays attention to our work. Hope our work can help you.**
