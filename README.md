# Word-Embeddings
{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyN1kiwoiFdMBRJA2uXxGdLO",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/WoraponSoontorn0/Word-Embeddings/blob/main/63114540197_07_Word_Embeddings.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "import nltk\n",
        "import gensim"
      ],
      "metadata": {
        "id": "1cblPQ_KuctG"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "nltk.download('wordnet')\n",
        "nltk.download('omw-1.4')\n",
        "from nltk.corpus import wordnet"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "Gr_AwPj9ugIR",
        "outputId": "9ff38826-ecda-466b-c2ac-79aff97dfb8d"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "[nltk_data] Downloading package wordnet to /root/nltk_data...\n",
            "[nltk_data]   Package wordnet is already up-to-date!\n",
            "[nltk_data] Downloading package omw-1.4 to /root/nltk_data...\n",
            "[nltk_data]   Package omw-1.4 is already up-to-date!\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "syns = wordnet.synsets('happy')"
      ],
      "metadata": {
        "id": "v5KoVPohuo1V"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "print(syns[1].name())"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "GhxG6qit0RAS",
        "outputId": "0c094a1e-0fa3-43cd-fdc5-ad245b28633f"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "felicitous.s.02\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "print(syns[1].lemmas()[0].name())"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "YGfWdOf900EV",
        "outputId": "be224a1a-cb72-4814-d356-5ff0f2ea0cc0"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "felicitous\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "print(syns[1].definition())"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "bx-RLtDC01SU",
        "outputId": "0bf4b99b-71c7-4582-ddf4-1e2d0f64c632"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "marked by good fortune\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "print(syns[0].examples())"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "UCyZWVKr04Ky",
        "outputId": "3006c4ae-cefc-42be-c53a-3870f4d00b98"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "['a happy smile', 'spent many happy days on the beach', 'a happy marriage']\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "synonyms = []\n",
        "antonyms = []\n",
        "\n",
        "for syn in wordnet.synsets('good'):\n",
        "  for e in syn.lemmas():\n",
        "    synonyms.append(e.name())\n",
        "    if e.antonyms():\n",
        "\n",
        "      antonyms.append(e.antonyms()[0].name())\n",
        "\n",
        "print(set(synonyms))\n",
        "print(set(antonyms))"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "kvT2Li7m07vm",
        "outputId": "c5e923c1-d7b8-4123-80fc-6b931dabe607"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "{'full', 'unspoilt', 'undecomposed', 'goodness', 'upright', 'well', 'safe', 'dear', 'commodity', 'effective', 'proficient', 'practiced', 'honest', 'trade_good', 'thoroughly', 'skillful', 'good', 'in_effect', 'honorable', 'soundly', 'unspoiled', 'beneficial', 'near', 'ripe', 'right', 'serious', 'in_force', 'expert', 'respectable', 'just', 'skilful', 'estimable', 'dependable', 'sound', 'salutary', 'adept', 'secure'}\n",
            "{'badness', 'bad', 'evil', 'ill', 'evilness'}\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "synonyms = []\n",
        "antonyms = []\n",
        "\n",
        "for syn in wordnet.synsets('good'):\n",
        "  for e in syn.lemmas():\n",
        "    synonyms.append(e.name())\n",
        "    if e.antonyms():\n",
        "\n",
        "      antonyms.append(e.antonyms()[0].name())\n",
        "\n",
        "print(set(synonyms))\n",
        "print(set(antonyms))"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "2fv1hxD065Qu",
        "outputId": "9e38d202-9f2e-4c05-d888-4523380e3a26"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "{'full', 'unspoilt', 'undecomposed', 'goodness', 'upright', 'well', 'safe', 'dear', 'commodity', 'effective', 'proficient', 'practiced', 'honest', 'trade_good', 'thoroughly', 'skillful', 'good', 'in_effect', 'honorable', 'soundly', 'unspoiled', 'beneficial', 'near', 'ripe', 'right', 'serious', 'in_force', 'expert', 'respectable', 'just', 'skilful', 'estimable', 'dependable', 'sound', 'salutary', 'adept', 'secure'}\n",
            "{'badness', 'bad', 'evil', 'ill', 'evilness'}\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "syns[1].root_hypernyms()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "mq5OLg_A7BeP",
        "outputId": "cb1bf499-14f8-439c-d50c-6b18128748d7"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "[Synset('felicitous.s.02')]"
            ]
          },
          "metadata": {},
          "execution_count": 84
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "syns[1].pos()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        },
        "id": "wIXtO4qV7D2R",
        "outputId": "b27a8abb-e24a-4ed7-ebc7-1b666799c541"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "'s'"
            ],
            "application/vnd.google.colaboratory.intrinsic+json": {
              "type": "string"
            }
          },
          "metadata": {},
          "execution_count": 85
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "f = open('cell_phone.txt','r')\n",
        "data = []\n",
        "for line in f:\n",
        "  data.append(gensim.utils.simple_preprocess(line))\n",
        "f.close()"
      ],
      "metadata": {
        "id": "9UItg9b43DJI"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "model = gensim.models.Word2Vec(window=10,min_count=2,workers=4)"
      ],
      "metadata": {
        "id": "_dkwLBMu4Iz7"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "model.build_vocab(data, progress_per=1000)"
      ],
      "metadata": {
        "id": "t6F4LW9m4LoJ"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "model.train(data,total_examples=model.corpus_count,epochs=model.epochs)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "imlQKtYm4Vgu",
        "outputId": "0d62404e-0708-4248-ded1-321d76a9c082"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "(37734412, 53349715)"
            ]
          },
          "metadata": {},
          "execution_count": 89
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "model.save('myWord2Vec.model')"
      ],
      "metadata": {
        "id": "jzXQ3GlH4shJ"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "new_model = gensim.models.Word2Vec.load('myWord2Vec.model')"
      ],
      "metadata": {
        "id": "PPR84Gu14yIq"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "model.wv.get_vector('good')"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "0jN_N2Lr43hm",
        "outputId": "0c358d3e-1c3c-4781-ae5b-19238e047d1d"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([-3.6153083 , -0.15794685, -2.5050657 ,  3.1245625 , -0.7382892 ,\n",
              "        0.9477903 ,  0.6801793 , -0.20814808, -0.21644394, -0.8196619 ,\n",
              "       -3.641499  ,  1.1585667 ,  0.8021507 ,  0.35037187,  0.15859316,\n",
              "       -0.7101148 ,  1.2515447 , -0.4353719 , -0.05538597, -0.9571323 ,\n",
              "       -0.35202193, -3.624472  , -4.807286  , -4.320926  , -6.0436473 ,\n",
              "       -0.49845943,  1.4278629 ,  0.42300212,  0.91541725,  0.6937948 ,\n",
              "       -1.7567395 , -0.98230666, -0.8957907 ,  3.4296465 , -2.550455  ,\n",
              "       -2.0505676 , -0.28049487, -0.87701875,  0.57016766,  4.2653155 ,\n",
              "        1.1690991 ,  0.39526278, -0.46991086, -0.6399785 , -0.15808538,\n",
              "       -0.00690804,  2.465327  , -1.427262  , -2.7857552 ,  4.0925407 ,\n",
              "       -0.5193617 ,  0.07049873, -2.3846357 ,  2.019107  ,  0.80478257,\n",
              "       -1.5166348 ,  0.4840398 ,  3.3257558 ,  2.770121  ,  2.3923397 ,\n",
              "       -4.3593373 ,  1.2257403 , -2.212798  ,  0.99328786,  0.2834914 ,\n",
              "       -0.9403538 , -0.50811404, -0.9311118 ,  1.3919832 , -1.8442302 ,\n",
              "       -2.2036014 , -3.9500906 , -1.2267148 , -0.8041775 ,  1.5358336 ,\n",
              "        3.5948453 , -1.7768152 , -0.80023396,  2.499118  , -1.5609944 ,\n",
              "        2.9947557 ,  0.55662423,  0.55339915, -5.1859403 ,  2.06202   ,\n",
              "        0.52704823, -3.1405356 , -2.822317  , -2.013356  ,  4.171061  ,\n",
              "        1.2679594 , -1.5100617 , -2.5163183 , -0.95657814, -1.9213412 ,\n",
              "       -0.4859206 , -0.5259355 , -1.465864  ,  0.5105219 ,  5.1613965 ],\n",
              "      dtype=float32)"
            ]
          },
          "metadata": {},
          "execution_count": 92
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "model.wv.most_similar('good')"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "067o42rz46i9",
        "outputId": "b1765f42-7063-442e-bbff-010db9837438"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "[('decent', 0.8045908212661743),\n",
              " ('great', 0.787036657333374),\n",
              " ('nice', 0.7228648662567139),\n",
              " ('bad', 0.689076840877533),\n",
              " ('excellent', 0.6479455232620239),\n",
              " ('poor', 0.6261720061302185),\n",
              " ('well', 0.5830737352371216),\n",
              " ('cool', 0.5727342963218689),\n",
              " ('weak', 0.5670397877693176),\n",
              " ('ok', 0.55568927526474)]"
            ]
          },
          "metadata": {},
          "execution_count": 93
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "model.wv.similarity('great', 'good')"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "LkgQI7d749Tg",
        "outputId": "36f8284a-8df7-4f25-b5a8-f8c169563738"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0.78703666"
            ]
          },
          "metadata": {},
          "execution_count": 94
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "model.wv.similarity('cheap', 'expensive')"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "cKTOA-WI4-kP",
        "outputId": "4f68215f-446e-4d14-9062-e98fbf200792"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0.47430873"
            ]
          },
          "metadata": {},
          "execution_count": 95
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "import gensim\n",
        "f = open('question_dataset.csv', encoding = 'utf8')\n",
        "data = []\n",
        "for line in f:\n",
        "  data.append(gensim.utils.simple_preprocess(line))\n",
        "f.close()\n",
        "data_for_training = []\n",
        "for i, list_of_words in enumerate(data):\n",
        "  tagged_doc = gensim.models.doc2vec.TaggedDocument(list_of_words, [i])\n",
        "  data_for_training.append(tagged_doc)\n",
        "model = gensim.models.doc2vec.Doc2Vec(vector_size=20,\n",
        "min_count=1,\n",
        "epochs=30\n",
        ")\n",
        "model.build_vocab(data_for_training)\n",
        "model.train(data_for_training,\n",
        "\n",
        "total_examples=model.corpus_count,\n",
        "epochs=model.epochs\n",
        ")\n",
        "\n",
        "model.save('my_doc2vec.model')"
      ],
      "metadata": {
        "id": "4voJe51O5G1G"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "model.wv.most_similar('phone')"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "G-jrHp385NI-",
        "outputId": "9d853b8f-4e65-487d-8524-0e885b9c7173"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "[('android', 0.9810728430747986),\n",
              " ('software', 0.9513051509857178),\n",
              " ('searching', 0.9340701103210449),\n",
              " ('preparing', 0.9319173097610474),\n",
              " ('internship', 0.9306079149246216),\n",
              " ('sbi', 0.9293165802955627),\n",
              " ('copy', 0.927191972732544),\n",
              " ('researchers', 0.9255433082580566),\n",
              " ('swe', 0.9227311611175537),\n",
              " ('free', 0.9215765595436096)]"
            ]
          },
          "metadata": {},
          "execution_count": 97
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "data_for_training[50]"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "laeNLYhn6YZH",
        "outputId": "57987875-4740-4c74-84fa-a3b16552f148"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "TaggedDocument(words=['is', 'career', 'launcher', 'good', 'for', 'rbi', 'grade', 'preparation'], tags=[50])"
            ]
          },
          "metadata": {},
          "execution_count": 98
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "model[50]"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "IQI7-DLT6ads",
        "outputId": "63653653-f542-4c27-904e-add038ee42b0"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([-0.23923264,  0.16381381,  0.11142684, -0.3781328 , -0.21581435,\n",
              "        0.00913053, -0.05374569, -0.09863573, -0.13416801,  0.18890464,\n",
              "        0.08265702,  0.14196606,  0.00863446, -0.25164992,  0.19599116,\n",
              "        0.19628437,  0.12750064,  0.07365007,  0.08178862, -0.02999797],\n",
              "      dtype=float32)"
            ]
          },
          "metadata": {},
          "execution_count": 99
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "model.docvecs.most_similar(50)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "pmkIJXKo6byB",
        "outputId": "117db34a-0ce3-4a5a-9403-edeeb1d3dbca"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "[(2398, 0.9910395741462708),\n",
              " (4847, 0.9906371831893921),\n",
              " (212, 0.9902102947235107),\n",
              " (4196, 0.9892800450325012),\n",
              " (4001, 0.9885634779930115),\n",
              " (1236, 0.988550066947937),\n",
              " (1087, 0.9878309965133667),\n",
              " (2627, 0.9877530336380005),\n",
              " (2376, 0.9871731996536255),\n",
              " (3412, 0.9871113300323486)]"
            ]
          },
          "metadata": {},
          "execution_count": 100
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "test_data = 'How to learn computer programming?'\n",
        "test_data = gensim.utils.simple_preprocess(test_data)\n",
        "test_vec = model.infer_vector(test_data)"
      ],
      "metadata": {
        "id": "ocP81CQU6ebp"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "test_similar = model.docvecs.most_similar([test_vec])\n",
        "print(test_similar)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "w26szSMj6jUR",
        "outputId": "b4f27c30-e985-434c-8bfe-1440e8e054e5"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "[(3280, 0.9047731161117554), (219, 0.8941574692726135), (884, 0.8396742343902588), (2164, 0.8393123149871826), (3383, 0.8343320488929749), (4511, 0.8277544975280762), (1638, 0.8201897144317627), (12, 0.8138708472251892), (3999, 0.799381673336029), (65, 0.7912759780883789)]\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [],
      "metadata": {
        "id": "6pO5GsgF6kyw"
      },
      "execution_count": null,
      "outputs": []
    }
  ]
}
