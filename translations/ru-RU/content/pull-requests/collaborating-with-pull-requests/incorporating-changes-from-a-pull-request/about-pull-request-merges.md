---
title: Сведения о слиянии запросов на вытягивание
intro: 'Вы можете [объединить запросы на вытягивание](/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request), сохранив все фиксации в ветви компонента, объединив все фиксации в одну фиксацию или перераспределив отдельные фиксации из ветви `head` в ветвь `base`.'
redirect_from:
  - /github/collaborating-with-issues-and-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges
  - /articles/about-pull-request-merge-squashing
  - /articles/about-pull-request-merges
  - /github/collaborating-with-issues-and-pull-requests/about-pull-request-merges
  - /github/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Pull requests
ms.openlocfilehash: 73f55f86a4b4b18828a767959e580abde87ea906
ms.sourcegitcommit: d697e0ea10dc076fd62ce73c28a2b59771174ce8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2022
ms.locfileid: '148099316'
---
## Слияние фиксаций

{% data reusables.pull_requests.default_merge_option %}

## Слияние фиксаций со сжатием

{% data reusables.pull_requests.squash_and_merge_summary %}

### Сообщение слияния для слияния со сжатием

{% ifversion default-merge-squash-commit-message %} Когда вы выполняете слияние со сжатием, {% data variables.product.prodname_dotcom %} создает сообщение о фиксации по умолчанию, которое можно изменять. В зависимости от конфигурации репозитория и количества фиксаций в запросе на вытягивание, не включая фиксации слияния, это сообщение может включать заголовок запроса на вытягивание, описание запроса на вытягивание или информацию о фиксациях.
{% else %} Когда вы выполняете слияние со сжатием, {% data variables.product.prodname_dotcom %} создает сообщение фиксации по умолчанию, которое можно изменять. Сообщение по умолчанию зависит от количества фиксаций в запросе на вытягивание, не включая фиксации слияния.

Количество фиксаций | Сводка | Описание |
----------------- | ------- | ----------- | 
Одна фиксация | Заголовок сообщения фиксации для одной фиксации плюс номер запроса на вытягивание | Основной текст сообщения фиксации для одной фиксации
Несколько фиксаций | Заголовок запроса на вытягивание плюс номер запроса на вытягивание | Список сообщений фиксации для всех сжимаемых фиксаций, упорядоченный по датам
{% endif %}

Количество фиксаций | Сводка | Описание |
----------------- | ------- | ----------- |
Одна фиксация | Заголовок сообщения фиксации для одной фиксации плюс номер запроса на вытягивание | Основной текст сообщения фиксации для одной фиксации
Несколько фиксаций | Заголовок запроса на вытягивание плюс номер запроса на вытягивание | Список сообщений фиксации для всех сжимаемых фиксаций, упорядоченный по датам

{% ifversion default-merge-squash-commit-message %} Люди с доступом координатора или администратора к репозиторию могут настроить сообщение слияния своего репозитория по умолчанию для всех фиксаций со сжатием, чтобы использовать заголовок запроса на вытягивание, заголовок запроса на вытягивание и сведения о фиксации или заголовок запроса на вытягивание и описание. Дополнительные сведения см. в разделе [Настройка сжатия фиксаций](/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests).{% endif %}

{% ifversion ghes = 3.6 %} Пользователи с правами администратора на доступ к репозиторию могут настраивать репозиторий так, чтобы использовать заголовок запроса на вытягивание в качестве сообщения слияния для всех фиксаций со сжатием. Дополнительные сведения см. в разделе [Настройка сжатия фиксаций](/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests).
{% endif %}

### Сжатие и слияние длительной ветви

Если после слияния запроса на вытягивание вы планируете продолжить работу с [головной ветвью](/github/getting-started-with-github/github-glossary#head-branch) запроса на вытягивание, запрос на вытягивание лучше не сжимать и не выполнять его слияние.

При создании запроса на вытягивание {% data variables.product.prodname_dotcom %} определяет последнюю фиксацию, которая присутствует и в головной, и в [базовой ветви](/github/getting-started-with-github/github-glossary#base-branch): фиксацию общего предка. При сжатии и слиянии запроса на вытягивание {% data variables.product.prodname_dotcom %} создает в базовой ветви фиксацию, которая содержит все изменения, внесенные в головной ветви после фиксации общего предка.

Поскольку эта фиксация присутствует только в базовой ветви, а в головной отсутствует, общий предок двух ветвей остается неизменным. Если вы продолжаете работать в головной ветви, создайте новый запрос на вытягивание между двумя ветвями. Он будет включать все фиксации после общего предка, включая фиксации, которые вы сжали и объединили в предыдущем запросе на вытягивание. Если конфликтов нет, эти фиксации можно безопасно объединить. Однако такой рабочий процесс повышает вероятность возникновения конфликтов слияния. Если вы будете и дальше сжимать и объединять запросы на вытягивание для длительной головной ветви, вам придется многократно разрешать одни и те же конфликты.

## Перемещение между ветвями и слияние фиксаций

{% data reusables.pull_requests.rebase_and_merge_summary %}

Вы не можете автоматически перебазировать и объединить данные {% variables.location.product_location %}, если:
- В запросе на вытягивание есть конфликты слияния.
- Перемещение фиксаций из базовой ветви в головную вызывает конфликты.
- Перемещение фиксаций считается небезопасным, например, если перемещение возможно без конфликтов слияния, но результат не будет таким же, как при слиянии.

Если вы по-прежнему хотите перебазировать фиксации, но не можете перебазировать и выполнить автоматическое слияние на {% данных variables.location.product_location %} необходимо:
- Переместите тематическую (или головную) ветвь в базовую ветвь локально в командной строке.
- [Устраните все конфликты слияния в командной строке](/articles/resolving-a-merge-conflict-using-the-command-line/).
- Принудительно отправьте перемещенные фиксации в тематическую (или удаленную головную) ветвь запроса на вытягивание.

Затем любой пользователь с разрешениями на запись в репозитории может [объединить изменения](/articles/merging-a-pull-request/) с помощью кнопки перебазы и слияния на {% данных variables.location.product_location %}.

## Непрямые слияния

Запрос на вытягивание можно объединить автоматически, если его головная ветвь напрямую или косвенно объединена в базовую ветвь за пределами. Другими словами, если фиксация чаевых головы становится доступной с кончика целевой ветви. Пример:

* Ветвь `main` находится в фиксации **C**.
* Ветвь `feature` была ветвлена `main` и в настоящее время находится на фиксации **D**. Эта ветвь имеет целевой запрос на вытягивание `main`.
* Ветвь `feature_2` отделяется от `feature` ветви и теперь находится в фиксации **E**. Эта ветвь также имеет целевой запрос на вытягивание `main`.

Если сначала выполняется слияние запроса на вытягивание **E** --> `main`, **запрос на** вытягивание D  --> `main` будет помечен как объединенный *автоматически*, так как все фиксации `feature` теперь доступны.`main` Слияние `feature_2` и `main` отправка `main` на сервер из командной строки помечает *оба* запроса на вытягивание как объединенные.

Запросы на вытягивание в этой ситуации будут помечены как `merged` даже если [правила защиты ветви](/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches#about-branch-protection-rules) не были выполнены.

## Дополнительные материалы

- [Сведения о запросах на вытягивание](/articles/about-pull-requests/)
- [Разрешение конфликтов слияния](/github/collaborating-with-pull-requests/addressing-merge-conflicts)
