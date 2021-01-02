#### [kvm-unit-tests PATCH] x86/access: Fixed test stuck issue on new 52bit machine
##### From: Yang Weijiang <weijiang.yang@intel.com>

```c
Content-Type: text/plain; charset="utf-8"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
X-Patchwork-Submitter: Yang Weijiang <weijiang.yang@intel.com>
X-Patchwork-Id: 12008945
Return-Path: <kvm-owner@kernel.org>
X-Spam-Checker-Version: SpamAssassin 3.4.0 (2014-02-07) on
	aws-us-west-2-korg-lkml-1.web.codeaurora.org
X-Spam-Level: 
X-Spam-Status: No, score=-16.8 required=3.0 tests=BAYES_00,
	HEADER_FROM_DIFFERENT_DOMAINS,INCLUDES_CR_TRAILER,INCLUDES_PATCH,
	MAILING_LIST_MULTI,SPF_HELO_NONE,SPF_PASS,USER_AGENT_GIT autolearn=ham
	autolearn_force=no version=3.4.0
Received: from mail.kernel.org (mail.kernel.org [198.145.29.99])
	by smtp.lore.kernel.org (Postfix) with ESMTP id BF4E8C433E0
	for <kvm@archiver.kernel.org>; Sun, 10 Jan 2021 09:09:05 +0000 (UTC)
Received: from vger.kernel.org (vger.kernel.org [23.128.96.18])
	by mail.kernel.org (Postfix) with ESMTP id 81F0423B00
	for <kvm@archiver.kernel.org>; Sun, 10 Jan 2021 09:09:05 +0000 (UTC)
Received: (majordomo@vger.kernel.org) by vger.kernel.org via listexpand
        id S1725956AbhAJJIt (ORCPT <rfc822;kvm@archiver.kernel.org>);
        Sun, 10 Jan 2021 04:08:49 -0500
Received: from mga12.intel.com ([192.55.52.136]:13938 "EHLO mga12.intel.com"
        rhost-flags-OK-OK-OK-OK) by vger.kernel.org with ESMTP
        id S1725807AbhAJJIs (ORCPT <rfc822;kvm@vger.kernel.org>);
        Sun, 10 Jan 2021 04:08:48 -0500
IronPort-SDR: 
 R4ELyBeOsOj9loycJda/NjbauaIyP02IpbybE9FKa0LpqMlXOF7SzlUcWEyEba/5hZ9ua1kbJn
 qN4dsAygA8fA==
X-IronPort-AV: E=McAfee;i="6000,8403,9859"; a="156933671"
X-IronPort-AV: E=Sophos;i="5.79,336,1602572400";
   d="scan'208";a="156933671"
Received: from orsmga008.jf.intel.com ([10.7.209.65])
  by fmsmga106.fm.intel.com with ESMTP/TLS/ECDHE-RSA-AES256-GCM-SHA384;
 10 Jan 2021 01:08:08 -0800
IronPort-SDR: 
 KP5jeN2C8Carec+zIm/PwpLs67WQUUwlWxk0W9mV3EIUf5B0IwyRzHqXhUnAOeg7I9Ir0frAb3
 IUW2FoWaSRHA==
X-ExtLoop1: 1
X-IronPort-AV: E=Sophos;i="5.79,336,1602572400";
   d="scan'208";a="380643426"
Received: from local-michael-cet-test.sh.intel.com ([10.239.159.149])
  by orsmga008.jf.intel.com with ESMTP; 10 Jan 2021 01:08:06 -0800
From: Yang Weijiang <weijiang.yang@intel.com>
To: pbonzini@redhat.com, kvm@vger.kernel.org
Cc: Yang Weijiang <weijiang.yang@intel.com>
Subject: [kvm-unit-tests PATCH] x86/access: Fixed test stuck issue on new
 52bit machine
Date: Sun, 10 Jan 2021 17:19:42 +0800
Message-Id: <20210110091942.12835-1-weijiang.yang@intel.com>
X-Mailer: git-send-email 2.17.2
Precedence: bulk
List-ID: <kvm.vger.kernel.org>
X-Mailing-List: kvm@vger.kernel.org

When the application is tested on a machine with 52bit-physical-address, the
synthesized 52bit GPA triggers EPT(4-Level) fast_page_fault infinitely. On the
other hand, there's no reserved bits in 51:max_physical_address on machines with
52bit-physical-address.

Signed-off-by: Yang Weijiang <weijiang.yang@intel.com>
---
 x86/access.c | 20 +++++++++++---------
 1 file changed, 11 insertions(+), 9 deletions(-)

```